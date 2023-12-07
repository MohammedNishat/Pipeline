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

        stage('Copying war file') {
            steps {
                echo "Copying war file"
                sh 'chmod o+w /opt/tomcat/webapps/'  // Optional: Adjust permissions if needed
                sh 'cp -v **/target/*.war /opt/tomcat/webapps/'
            }
        }

        stage('Deploy to Server') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '6414a1d2-f285-4e37-8439-908f9590548a', path: '', url: 'http://13.234.113.200:9090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
