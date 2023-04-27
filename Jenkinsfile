@Library('my-shared-library') _
pipeline
{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete',description: 'Choose Create/Destroy')
    }
    stages
    {
        when { expression { param.action == 'create' }}
        stage('GIT Checkout'){
            steps{
                script{
                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/THANUSHKIRAN/Java_Application_CICD.git"
                    )
                }
            }
        }
        stage('UNIT Test Maven')
        {
            when { expression { param.action == 'create' }}
            steps{
                script{
                    mvntest()
                }
            }
        }
        stage('MAVEN Integration Testing')
        {
            when { expression { param.action == 'create' }}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
        stage('Static Code Analysis')
        {
            when { expression { param.action == 'create' }}
            steps{
                script{
                    StaticCodeAnalysis()
                }
            }
        }
    }
}