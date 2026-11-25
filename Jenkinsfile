pipeline {
    agent any

    stages {
        stage('Clonage') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/wissalelhaydani/-CI_Project.git'
            }
        }

        stage('Verification Python') {
            steps {
                bat 'python --version'
                bat 'python -m pip --version'
            }
        }

        stage('Installation des dependances') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Analyse Qualite') {
            steps {
                bat 'python -m pylint calculator.py'
            }
        }

        stage('Tests unitaires') {
            steps {
                bat 'python -m pytest -v'
            }
        }
    }

    post {
        always {
            echo 'Pipeline termine'
        }
        success {
            echo 'BUILD SUCCESS'
        }
        failure {
            echo 'BUILD FAILED'
        }
    }
}