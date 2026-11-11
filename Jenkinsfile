

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
                     mkdir -p /var/www/html
                    cp index.html /var/www/html/index.html
                '''
            }
        }
    }
}


