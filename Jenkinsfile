pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ayush-Singh986/Docker-Project.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t blogging-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f blogging-app || true
                docker run -d -p 8081:80 --name blogging-app blogging-app
                '''
            }
        }

        stage('Docker Push') {
            steps {
                withDockerRegistry(
                    credentialsId: 'docker-cred',
                    url: 'https://index.docker.io/v1/'
                ) {
                    sh '''
                    docker tag blogging-app ayush244/blogging-app:latest
                    docker push ayush244/blogging-app:latest
                    '''
                }
            }
        }
    }
}
