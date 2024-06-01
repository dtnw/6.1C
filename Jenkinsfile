pipeline{
    agent any
    environment {
        DIRECTORY_PATH = "C:/Users/derby/Documents/Deakin 2024/Code"
    }
     triggers {
        pollSCM('H/5 * * * *') // Poll every 5 minutes
    }
    stages{
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dtnw/6.1C.git'
            }
        }
        stage('Build'){
            steps{
                echo "Fetch the source code from ${env.DIRECTORY_PATH}."
                echo "Build the code using Maven to compile and package the code."
            }
        }
        stage('Unit and Integration Tests'){
            steps {
                script {
                    try {
                        echo "Run unit tests using JUnit to ensure the code functions as expected."
                        echo "Run integration tests using Selenium to ensure different components of the application work together as expected."
                        bat 'echo "The unit and integration tests have been successfully completed." > logs.txt' // Success logs
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        bat 'echo "The unit and integration tests have failed." > logs.txt' // Fail logs
                        throw e
                    }
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: 'logs.txt', allowEmptyArchive: true
                }
                success {
                    emailext(
                        subject: "Test Status: SUCCESS",
                        body: "The unit and integration tests have completed successfully. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
                failure {
                    emailext(
                        subject: "Test Status: FAILURE",
                        body: "The unit and integration tests have failed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
            }
        }
    }
}