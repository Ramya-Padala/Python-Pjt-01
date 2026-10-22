pipeline {
agent any 
stages {
stage('clone git repo') {
steps {
https://github.com/Ramya-Padala/Python-Pjt-01.git
}
}
stage('Install Python Dependencies & Test') {
steps {
sh '''
apt install python3 python3-pip python3-venv -y
python3 -m venv venv
source venv/bin/activate
python -m pip install Flask
python -m flask --version
sh '''
}
}
stage('Build Docker Image & Start Docker Container') {
steps {
sh '''
docker build -t flask-app:latest .'
docker stop flask-container || true
docker rm flask-container || true
docker run -d -p 5000:5000 --name flask-container flask-app:latest
sh '''
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
}
}
