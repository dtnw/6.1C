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
                echo "Compile the code and generate any necessary artifacts."
            }
        }
        stage('Test'){
            steps{
                echo "Unit tests"
                echo "Integration tests"
            }
        }
        stage('Code Quality Check'){
            steps{
                    echo "Check the quality of the code."
                  }
            }
        stage('Deploy'){
            steps{
                    echo "Deploy the application to ${env.TESTING_ENVIRONMENT}"
                  }
            }
        stage('Approval'){
            steps{
                    script {
                    sleep(10)
                }
                echo "Manual approval success"
                  }
            }
        stage('Deploy to Production'){
            steps{
                    echo "Deploy the application to ${env.PRODUCTION_ENVIRONMENT}"
                  }
            post {
                always {
                    emailext(
                        subject: "Deployment Status: ${currentBuild.result}",
                        body: "The deployment to production has completed. Build status: ${currentBuild.result}.",
                        to: 'derbyt.uni@gmail.com',
                    )
                }
            }
        }
    }
}
