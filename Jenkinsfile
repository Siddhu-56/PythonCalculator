pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Python') {
            steps {
                bat 'python --version'
                bat 'python -m pip --version'
            }
        }

        stage('Upgrade pip') {
            steps {
                bat 'python -m pip install --upgrade pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Install PyInstaller') {
            steps {
                bat 'python -m pip install pyinstaller'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'python -m unittest discover -v'
            }
        }

        stage('Create EXE') {
            steps {
                bat 'python -m PyInstaller --clean --onefile calculator.py'
            }
        }

        stage('Archive EXE') {
            steps {
                archiveArtifacts artifacts: 'dist/*.exe',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build Successful'
            echo 'calculator.exe has been created and archived.'
        }

        failure {
            echo 'Build Failed'
        }

        always {
            echo 'Pipeline Finished'
        }
    }
}