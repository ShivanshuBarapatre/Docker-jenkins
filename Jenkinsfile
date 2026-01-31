pipeline {
    agent {
        docker {
            image 'python:3.10'
            args '-u root'
        }
    }

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests & Coverage') {
            steps {
                sh 'pytest --cov=app --cov-report=xml tests/'
            }
        }
    }

    post {
        always {
            deleteDir()   // safer than cleanWs in docker agent
        }
    }
}
