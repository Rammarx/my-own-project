pipeline{
    agent any
    environment {
        VERSION = "${env.BUILD_NUMBER}"
    }
    stages{
        stage("sonar-qube test"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar'){
                         sh 'chmod +x gradlew'
                         sh './gradlew sonarqube'
                    }
                    /** 

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }

                    
                }
                
            }
            
        }
        
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
        
        stage('Hello') {
            steps {
                 script{
                     sh 'sudo kubectl get nodes'
                 } 
            }
        }
    
        
    }
    post {
		always {
			mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "ram.amazon.mail@gmail.com";  
		}
	}
    
}
