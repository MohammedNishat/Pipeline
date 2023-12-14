pipeline {
    agent any
    tools {
        maven 'maven_home'
    }

    environment {
        TOMCAT_SERVER = '13.51.6.164'
        TOMCAT_PORT = '9090'
        TOMCAT_CREDENTIALS_ID = '21f67f4c-1b60-4cd3-8baa-43e963a1b259' // Jenkins credentials ID for Tomcat authentication
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Customize Maven goals and options as needed
                    sh "mvn clean package"
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Copy the WAR file to the Tomcat server using SCP or any other method
                    withCredentials([usernamePassword(credentialsId: TOMCAT_CREDENTIALS_ID, passwordVariable: 'TOMCAT_PASSWORD', usernameVariable: 'TOMCAT_USER')]) {
                        sh "scp -i //home/ec2-user/key.pem target/JenkinsWar.war nishat@13.51.6.164:/opt/tomcat/webapps/Jenkins.war"
                    }

                    // Trigger Tomcat to deploy the WAR file
                    sh "curl --upload-file target/*.war http://${TOMCAT_USER}:${TOMCAT_PASSWORD}@${TOMCAT_SERVER}:${TOMCAT_PORT}/manager/text/deploy?path=/Jenkins"
                }
            }
        }
    }
}
