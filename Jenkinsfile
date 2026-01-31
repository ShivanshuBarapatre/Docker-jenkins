pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Python') {
            steps {
                sh '''
                apt-get update
                apt-get install -y python3 python3-pip
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }

        stage('Run Tests & Coverage') {
            steps {
                sh 'python3 -m pytest --cov=app --cov-report=xml tests/'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
