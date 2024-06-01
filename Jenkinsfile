pipeline{
    agent any
    environment {
        DIRECTORY_PATH = "C:/Users/derby/Documents/Deakin 2024/Code"
        TESTING_ENVIRONMENT = "Testing environment: SIT753"
        PRODUCTION_ENVIRONMENT = "Derby"
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
        stage('Test'){
            steps {
                script {
                    try {
                        echo "Run unit tests to ensure the code functions as expected."
                        echo "Run integration tests to ensure different components of the application work together as expected."
                        bat 'echo "The unit and integration tests have completed.
                        Build status: ${currentBuild.result}." > test-logs.txt' // Replace with actual test command
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        bat 'echo "Test failed logs" > test-logs.txt' // Replace with actual failure log
                        throw e
                    }
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: 'test-logs.txt', allowEmptyArchive: true
                    emailext(
                        subject: "Test Status: ${currentBuild.result}",
                        body: "The unit and integration tests have completed. Build status: ${currentBuild.currentResult}.",
                        to: 'derbyt.uni@gmail.com',
                        attachmentsPattern: 'test-logs.txt'
                    )
                }
            }
        }
        stage('Code Analysis'){
            steps{
                    echo "Integrate _________ to analyse the code and ensure it meets industry standards."
                  }
            }
        stage('Security Scan'){
            steps{
                    echo "Perform a security scan on the code using __________ to identify any vulnerabilities."
                  }
            
            post {
                always {
                    emailext(
                        subject: "Security Scan Status: ${currentBuild.result}",
                        body: "The security scan has completed. Build status: ${currentBuild.result}.",
                        to: 'derbyt.uni@gmail.com',
                    )
                }
            }
        }
        stage('Deplay to Staging'){
            steps{
                echo "Deploy the application to a staging server (AWS EC2 instance etc)."
                  }
            }
        stage('Integration Tests on Staging'){
            steps{
                echo "Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment."
                  }
            }
        stage('Deploy to Production'){
            steps{
                    echo "Deploy the application to a production server (e.g.)"
                  }
            
        }
    }
}
