 pipeline {
    agent any
      tools {
        maven 'local_home'
    }

    environment {
        TOMCAT_SERVER = 'http://13.51.6.164:9090/'
        TOMCAT_PORT = '9090'
        TOMCAT_CREDENTIALS_ID = deploy adapters:'deploy adapters: [tomcat9(credentialsId: '21f67f4c-1b60-4cd3-8baa-43e963a1b259', path: '', url: 'http://13.51.6.164:9090/')], contextPath: null, war: '"**/*.war"'' // Jenkins credentials ID for Tomcat authentication
    }

    stages {
        stage('Build') {
            steps {
                // Maven build
                script {
                    
                    // Customize Maven goals and options as needed
                    sh " clean package"
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Copy the WAR file to the Tomcat server using SCP or any other method
                    withCredentials([usernamePassword(credentialsId: TOMCAT_CREDENTIALS_ID, passwordVariable: 'TOMCAT_PASSWORD', usernameVariable: 'TOMCAT_USER')]) {
                        sh "scp target/Jenkins.war ${TOMCAT_USER}@${TOMCAT_SERVER}:/opt/tomcat/webapps"
                    }

                    // Trigger Tomcat to deploy the WAR file
                    sh "curl http://${TOMCAT_USER}:${TOMCAT_PASSWORD}@${TOMCAT_SERVER}:${TOMCAT_PORT}/manager/text/deploy?path=/Jenkins.war"
                }
            }
        }
    }
}
