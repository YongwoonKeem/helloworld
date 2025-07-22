pipeline {
    agent any
    tools {
        nodejs 'Node18'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/YongwoonKeem/helloworld.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('yongwoonkeem/helloworld')
                }
            }
        }
        stage('Push Docker Image') {
            when {
                branch 'main'
            }
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('yongwoonkeem/helloworld').push('latest')
                    }
                }
            }
        }
    }
}
