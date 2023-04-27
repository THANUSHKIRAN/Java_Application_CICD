@Library('my-shared-library') _
pipeline
{
    agent any
    stages
    {
        stage('GIT Checkout'){
            steps{
                script{
                    gitCheckout(
                        branch: "main"
                        url: "https://github.com/THANUSHKIRAN/Java_Application_CICD.git"
                    )
                }
            }
        }
    }
}