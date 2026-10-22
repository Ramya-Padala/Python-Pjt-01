pipeline {
agent any 
stages {
stage('clone git repo') {
steps {
    git branch: 'main',
url: 'https://github.com/Ramya-Padala/Python-Pjt-01.git'
}
}
stage('Install Python Dependencies & Test') {
 steps {
        sh '''
            python3 --version
            python3 -m venv venv
            ./venv/bin/python -m pip install Flask
            ./venv/bin/python -m flask --version
        '''
}
}
stage('Build Docker Image & Start Docker Container') {
steps {
sh '''
docker build -t flask-app:latest .
docker stop flask-container || true
docker rm flask-container || true
docker run -d -p 5000:5000 --name flask-container flask-app:latest
'''
}
}
}
post {
success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Deployment failed. Check the logs.'
        }
    }
}

