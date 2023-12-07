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

        stage('Deploy to Server') {
            steps {
                script {
                    def tomcatAdapters = [
                        [$class: 'Tomcat9xAdapter', credentialsId: '6414a1d2-f285-4e37-8439-908f9590548a', path: '', url: 'http://65.2.170.40:9090/']
                        // Add more adapters if needed
                    ]

                    def deployParams = [
                        adapters: tomcatAdapters,
                        contextPath: 'JenkinsWar',  // Adjust context path as needed
                        war: '**/*.war'
                    ]

                    step([$class: 'CargoContainerPublisher', deployer: [$class: 'Tomcat9xRemoteDeployer', parameters: deployParams]])
                }
            }
        }
    }
}
