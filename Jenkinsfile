@Library('my-shared-library') _
pipeline
{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete',description: 'Choose Create/Destroy')
    }
    stages
    {
        
        stage('GIT Checkout'){
            when { expression { params.action == 'create' }}
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
            when { expression { params.action == 'create' }}
            steps{
                script{
                    mvntest()
                }
            }
        }
        stage('MAVEN Integration Testing')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
        stage('Static Code Analysis')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    def SonarQubecredentialsId='sonar-api'
                    StaticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
        stage('Quality Gate Check')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    def QualityGateStatuscredentialsId='sonar-api'
                    QualityGateStatus(QualityGateStatuscredentialsId)
                }
            }
        }
        stage('Maven Build')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    
                    mvnBuild()
                }
            }
        }

    }
}