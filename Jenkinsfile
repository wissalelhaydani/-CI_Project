pipeline {
    agent any

    stages {
        stage('Clonage') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/wissalelhaydani/-CI_Project.git'
            }
        }

        stage('Vérification Python') {
            steps {
                bat 'python --version'
                bat 'python -m pip --version'
            }
        }

        stage('Installation des dépendances') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Analyse qualité du code') {
            steps {
                bat 'python -m pylint calculator.py || exit /b 0'
            }
        }

        stage('Tests unitaires') {
            steps {
                bat 'python -m pytest'
            }
        }

        stage('Création de l artefact') {
            steps {
                bat '''
                if exist Release rmdir /S /Q Release
                mkdir Release

                copy calculator.py Release
                copy test_calculator.py Release
                copy requirements.txt Release
                powershell Compress-Archive -Path Release\\* -DestinationPath Release.zip -Force
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé'
        }
        success {
            echo 'BUILD SUCCESS'
        }
        failure {
            echo 'BUILD FAILED'
        }
    }
}