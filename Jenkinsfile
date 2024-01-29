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
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/nsekhar73/edureka-java-project.git'
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
  }
}
