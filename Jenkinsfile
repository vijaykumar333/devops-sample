def
	giturl = 'https://github.com/vennavenkatesh/devops-sample.git'
	branch_name = 'master'

pipeline {
    agent any
    
    parameters {
        string(name: 'IP', description: 'Please enter you backend IP')
    }
    stages {
        stage("Git checkout") {
            steps {
                echo "checkout the code from bitbucket"
                git branch: "$branch_name", url: "$giturl" , poll: true
            }
        }

        stage("Test-cases & Build") {
            steps {
                echo "executing the test cases"
                sh "cd $WORKSPACE && mvn clean install"
            }
        }

        stage("Backup") {
            steps {
                echo "Print the workspave path"
                echo "Hello ${params.NAME}"
                sh "echo $WORKSPACE"
                sh '''
                #!/bin/bash
                ssh tomcat@$IP << EOF
                cd /opt/apache-tomcat-8.5.72/webapps
                mv *.war /opt/apache-tomcat-8.5.72/backup
                exit 0
                EOF'''
            }

        }

        stage("Deploy-tomcat-server") {
            steps {
                echo "Deploy into tomcat server"
                
                echo " Deployment has been completed successfully"
            }    
        }
    }
}
