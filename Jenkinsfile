pipeline{
    agent any
    environment {
        DIRECTORY_PATH = "C:/Users/derby/Documents/Deakin 2024/Code"
    }
     triggers {
        pollSCM('H/3 * * * *') // Poll every 3 minutes
    }
    stages{
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dtnw/6.1C.git'
                echo "test 2."
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
        stage('Code Analysis'){
            steps{
                    echo "Integrate SonarQube to analyse the code and ensure it meets industry standards."
                  }
            }
        stage('Security Scan'){
            steps {
                script {
                    try {
                        echo  "Perform a security scan on the code using OWASP Zap to identify any vulnerabilities."
                        bat 'echo "The security scans have been successfully completed." > logs.txt' // Success logs
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        bat 'echo "The security scans have failed." > logs.txt' // Fail logs
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
                        subject: "Scan Status: SUCCESS",
                        body: "The security scans have been successfully completed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
                failure {
                    emailext(
                        subject: "Scan Status: FAILURE",
                        body: "The security scans have failed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
            }
        }
        stage('Deplay to Staging'){
            steps{
                echo "Deploy the application to a staging server on AWS EC2 instance."
                  }
            }
        stage('Integration Tests on Staging'){
            steps {
                script {
                    try {
                        echo  "Run integration tests on the staging environment (AWS EC2 instance) to ensure the application functions as expected in a production-like environment."
                        bat 'echo "The integration tests on staging have been successfully completed." > logs.txt' // Success logs
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        bat 'echo "The integration tests on staging have failed." > logs.txt' // Fail logs
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
                        body: "The integration tests on staging have been successfully completed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
                failure {
                    emailext(
                        subject: "Test Status: FAILURE",
                        body: "The integration tests on staging have failed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'logs.txt'
                    )
                }
            }
        }
        stage('Deploy to Production'){
            steps{
                    echo "Deploy the application to a production server on AWS EC2 instance."
                  }
        }
    }
}