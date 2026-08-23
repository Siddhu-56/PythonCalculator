pipeline {
    agent any

    environment {
        PYTHON_EXE = 'C:\\Users\\SIDDU\\AppData\\Local\\Programs\\Python\\Python314\\python.exe'
    }

    stages {

        stage('Verify Python') {
            steps {
                bat '"%PYTHON_EXE%" --version'
                bat '"%PYTHON_EXE%" -m pip --version'
            }
        }

        stage('Upgrade pip') {
            steps {
                bat '"%PYTHON_EXE%" -m pip install --upgrade pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"%PYTHON_EXE%" -m pip install -r requirements.txt'
            }
        }

        stage('Install PyInstaller') {
            steps {
                bat '"%PYTHON_EXE%" -m pip install pyinstaller'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat '"%PYTHON_EXE%" -m unittest discover -v'
            }
        }

        stage('Create EXE') {
            steps {
                bat '"%PYTHON_EXE%" -m PyInstaller --clean --onefile calculator.py'
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