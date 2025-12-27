pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/Sachin1652/secretsanta-generator'
            }
        }

        stage('Code Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Pipeline Status: ${BUILD_NUMBER}",
                body: '''
                    <html>
                        <body>
                            <p>Build Status: ${BUILD_STATUS}</p>
                            <p>Build Number: ${BUILD_NUMBER}</p>
                            <p>
                                Check the 
                                <a href="${BUILD_URL}">console output</a>.
                            </p>
                        </body>
                    </html>
                ''',
                to: 'sachinraj1652@gmail.com',
                from: 'jenkins@example.com',
                replyTo: 'jenkins@example.com',
                mimeType: 'text/html'
            )
        }
    }
}
