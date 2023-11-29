pipeline{
    agent any
    tools{
        maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts : '**/target/*.war'
                }
            }
        }
        stage('Deploy to Server'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat_credential', path: '', url: 'http://16.171.152.20:7070/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
