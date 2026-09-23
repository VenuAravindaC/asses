pipeline {
    agent { 
        label 'windows' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                python -m venv venv
                call venv\\Scripts\\activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '''
                call venv\\Scripts\\activate
                pytest test_app.py --junitxml=results.xml
                '''
            }
        }
    }

    post {
        success {
            echo ' Build Successful!'
        }
        failure {
            echo ' Build Failed!'
        }
    }
}
