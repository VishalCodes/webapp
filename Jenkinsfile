pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                        echo "PATH = ${PATH}"
                        echo "M2_HOME = ${M2_HOME}"
                   ''' 
            }
        }

        stage ('Build stage') {
            steps {
            sh 'mvn clean package'
            }
        }

        stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@52.88.238.144:/prod/apache-tomcat-8.5.66/webapps/webapp.war'
              }      
           }       
        }

        
    }
}