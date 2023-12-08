pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying the artifact to Tomcat"
                script {
                    def tomcatCredentialsId = '0c5f1030-10b2-4491-bb6e-d0676790f256'
                    def tomcatUrl = 'http://15.206.205.119:9090/'
                    def warFile = 'target/*.war'

                    tomcat9Deploy adapters: [tomcat9(credentialsId: tomcatCredentialsId, path: '', url: tomcatUrl)],
                                contextPath: null,
                                war: warFile
                }
            }
        }
    }
}
