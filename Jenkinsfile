pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/CICD-practice.git'
            }
        }

        stage('Build') {
            steps {
                sh 'cd helllo-jenkins && mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'cd helllo-jenkins && mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'cd helllo-jenkins && mvn package'
            }
        }

        // Optional Docker stage for deployment
        stage('Docker Build & Run') {
            steps {
                sh '''
                cd helllo-jenkins
                docker build -t hello-jenkins-app .
                docker stop hello-jenkins-container || true
                docker rm hello-jenkins-container || true
                docker run -d --name hello-jenkins-container hello-jenkins-app
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully ✅'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}

