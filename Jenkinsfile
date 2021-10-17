pipeline {
    agent { label 'master' }
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub-ayassawy')
    }

    stages {

        stage('Checkout') {
            steps{
                git branch: 'main', url: 'git@github.com:Ayassawy/jenkins-public.git'
            }
        }

        stage('Build') {
            steps{
                sh 'docker build -t devops14:latest .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('ImageTag') {
            steps {
                sh 'docker tag devops14:latest ayassawy/devops14-docker:version2'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push ayassawy/devops14-docker:version2'
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
