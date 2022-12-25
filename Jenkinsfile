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
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                         sh 'chmod +x gradlew'
                         sh './gradlew sonarqube'
                    }
                }
                
            }
            
        }
    }
    
}
