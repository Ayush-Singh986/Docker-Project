pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ayush-Singh986/Docker-Project.git'
            }
        }

        stage('Build & Run') {
            steps {
                sh '''

                docker build -t blogging-app .

                docker rm -f blogging-app

                docker run -d -p 8080:80 --name blogging-app blogging-app
                '''
            }
        }
    }
}
