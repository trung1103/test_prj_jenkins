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

    post {
        success {
            emailext(
                subject: "BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> thanh cong.</p>
                         <p><a href="${env.BUILD_URL}">Xem chi tiet</a></p>""",
                to: 'linhtrung3011@gmail.com',
                mimeType: 'text/html'
            )
        }
        failure {
            emailext(
                subject: "BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> THAT BAI.</p>
                         <p><a href="${env.BUILD_URL}console">Xem console log</a></p>""",
                to: 'linhtrung3011@gmail.com',
                mimeType: 'text/html'
            )
        }
    }
}
