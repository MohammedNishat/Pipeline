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
                    def tomcatUrl = 'http://15.206.205.119:9090'
                    def warFile = 'target/*.war'
                    def tomcatManagerCredentials = 'nishat1:nishat'  

                    sh """
                        curl --upload-file ${warFile} \
                             --user ${tomcatManagerCredentials} \
                             ${tomcatUrl}/manager/text/deploy?path=/JenkinsWar
                    """
                }
            }
        }
    }
}
