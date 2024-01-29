pipeline {
    agent { label 'Agent' }
    tools {
        jdk 'Java 17'
        maven 'Maven3'
    }
stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/nsekhar73/register-app.git'
                }
           }
        

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }

      stage("SonarQube Analysis"){
           steps {
	           script {
		        withSonarQubeEnv(credentialsId: 'Jenkins-Sonarqube-token') { 
                        sh "mvn sonar:sonar"
		        }
	           }	
           }
       }

	stage("Quality Gate"){
           steps {
               script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Jenkins-Sonarqube-token'
                }	
            }

        }
  }
}
