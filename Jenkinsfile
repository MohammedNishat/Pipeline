pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
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
deploy adapters: [tomcat9(credentialsId: '85531fb9-441f-4720-8a90-9e0cc03ac1d1', path: '', url: 'http://http://3.109.152.239:9090/')], contextPath: 'App', war: '**/*.war*'            }
        }
    }
}
