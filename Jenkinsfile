pipeline{
    agent any
    stages{
        stage("sonar-qube test"){
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
