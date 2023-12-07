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
deploy adapters: [tomcat9(credentialsId: '6414a1d2-f285-4e37-8439-908f9590548a', path: '', url: 'http://3.109.152.239:9090/')], contextPath: 'JenkinsWar', war: '**/*.war'        }
    }
}
