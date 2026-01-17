pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ayush-Singh986/Docker-Project.git'
            }
        }

        stage('Docker Login') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'docker-cred',
            usernameVariable: 'USER',
            passwordVariable: 'PASS'
        )]) {
            sh 'echo $PASS | docker login -u $USER --password-stdin'
        }
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
                sh '''
                docker tag blogging-app ayushsingh986/blogging-app
                docker push ayushsingh986/blogging-app
                '''
            }
        }
    }
}
