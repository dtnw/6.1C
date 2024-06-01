pipeline{
    agent any
    environment {
        DIRECTORY_PATH = "C:/Users/derby/Documents/Deakin 2024/Code"
        TESTING_ENVIRONMENT = "Testing environment: SIT753"
        PRODUCTION_ENVIRONMENT = "Derby"
    }
    stages{
        stage('Build'){
            steps{
                echo "Fetch the source code from ${env.DIRECTORY_PATH}."
                echo "Build the code using Maven to compile and package the code."
            }
        }
        stage('Test'){
            steps{
                echo "Run unit tests to ensure the code functions as expected."
                echo "Run integration tests to ensure different components of the application work together as expected."
            }
        }
        post {
                always {
                    emailext(
                        subject: "Test Status: ${currentBuild.result}",
                        body: "The unit and integration tests has completed. Build status: ${currentBuild.result}.",
                        to: 'derbyt.uni@gmail.com',
                    )
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
