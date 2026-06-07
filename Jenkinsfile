pipeline {
    agent any

    environment {
        APP_NAME = 'test_prj_jenkins'
        EXE_PATH = 'build\\test_prj_jenkins.exe'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat '''
                    if not exist build mkdir build
                    g++ -o %EXE_PATH% main.cpp -std=c++17
                '''
            }
        }

        stage('Test') {
            steps {
                bat '%EXE_PATH%'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build\\*.exe',
                                 fingerprint: true,
                                 onlyIfSuccessful: true
            }
        }
    }

}
