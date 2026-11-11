

pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/NITHYAVEL04/Auto-Deploy-Website-with-GitHub-Jenkins-and-AWS.git'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    sudo mkdir -p /var/www/html
                    sudo cp index.html /var/www/html/index.html
                '''
            }
        }
    }
}
