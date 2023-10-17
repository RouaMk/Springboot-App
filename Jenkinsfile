pipeline {
    agent any

  
    stages {
        stage('Checkout Code from GitHub') {
            steps {
               
                checkout([$class: 'GitSCM', 
                    branches: [[name: 'main']], 
                    userRemoteConfigs: [[url: 'https://github.com/RouaMk/Springboot-App.git']]
                ])
            }
        }

        stage('Build and Package Application') {
            steps {
             
              sh 'mvn clean package'
               
            } 
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-spring-app .'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                // Connectez-vous à Docker Hub
                withDockerRegistry([credentialsId: 'RouaMk', url: 'https://index.docker.io/v1/']) {
                    
                    sh 'docker push my-spring-app'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline terminé avec succès.'
        }
        failure {
            echo 'Échec du pipeline. Veuillez vérifier les étapes précédentes.'
        }
    }
}
