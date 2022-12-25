pipeline{
    agent any
    stages{
        stage("sonar-qube test"){
            agent {
                docker {
                    image 'openjdk:11'
                }
            }
            steps{
                withSonarQubeEnv(credentialsId: 'sonar-pass') {
                     sh 'chmod +x gradlew'
                     sh './gradlew sonarqube'
    
                 }
                
            }
            
        }
    }
    
}
