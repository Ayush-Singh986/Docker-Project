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
                if ! command -v docker >/dev/null 2>&1; then
                  echo "Docker not found. Install Docker and give Jenkins access to it."
                  exit 1
                fi

                docker build -t blogging-app .

                docker rm -f blogging-app || true

                docker run -d -p 8080:80 --name blogging-app blogging-app
                '''
            }
        }
    }
}
