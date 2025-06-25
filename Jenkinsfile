pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kishan-Prakash/model-train.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // sh 'pip install -r requirements.txt'
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''

            }
        }
        stage('Train Model') {
            steps {
                sh './venv/bin/python train.py'
            }
        }
        stage('Test Model') {
            steps {
                sh './venv/bin/python test.py'
            }
        }
        stage('Archive Model') {
            steps {
                archiveArtifacts artifacts: 'diabetes_model.pkl', fingerprint: true
            }
        }
    }
}