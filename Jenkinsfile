pipeline{
    agent any
    environment {
        VERSION = "${env.BUILD_NUMBER}"
    }
    stages{
        stage("sonar-qube test"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar') {
                         sh 'chmod +x gradlew'
                         sh './gradlew sonarqube'
                    }

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForqualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }

                    
                }
                
            }
            
        }
        /** 
        stage("docker login and docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker-pass', variable: 'docker')]) {
                        sh '''
                            docker build -t 52.66.45.157:8083/springapp:${VERSION} .
                            docker login -u admin -p $docker 52.66.45.157:8083
                            docker push 52.66.45.157:8083/springapp:${VERSION}
                            docker rmi 52.66.45.157:8083/springapp:${VERSION}
                        '''
    
                    }
                     

                }
            }
        }
        **/
    }
    
}
