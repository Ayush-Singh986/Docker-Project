pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ayush-Singh986/Docker-Project.git'
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
                docker rm -f blogging-app 
                docker run -d -p 8080:80 --name blogging-app blogging-app
                '''
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                docker tag blogging-app ayushsingh986/blogging-app
                docker login
                docker push ayushsingh986/blogging-app
                '''
            }
        }
    }
}
