@Library('my-shared-library') _
pipeline
{
    agent any
    parameters{
        choice(name: 'action', choices: 'create\ndelete',description: 'Choose Create/Destroy')
        string(name: 'ImageName', description: "Name of the docker build" ,defaultValue: 'JavaCICDApp')
        string(name: 'ImageTag', description: "Tag of the docker build" ,defaultValue: 'v1')
        string(name: 'UserName', description: "Name of the User" ,defaultValue: 'springboot')
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
                    def SonarQubecredentialsId='project1'
                    StaticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }
        stage('Quality Gate Check')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    def QualityGateStatuscredentialsId='project1'
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

        stage('Docker Image Build')
        {
            when { expression { params.action == 'create' }}
            steps{
                script{
                    
                    dockerBuild("${params.ImageName}","${params.ImageTag}","${params.UserName}")
                }
            }
        }

    }
}