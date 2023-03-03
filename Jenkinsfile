Skip to content
Search or jump to…
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@Iman-khayat 
henrikboulund
/
CalculatorPipeline
Public
forked from tboulund-devops/CalculatorPipeline
Fork your own copy of henrikboulund/CalculatorPipeline
Code
Pull requests
Actions
Projects
Security
Insights
Beta Try the new code view
CalculatorPipeline/Jenkinsfile
@henrikboulund
henrikboulund Update Jenkinsfile
Latest commit a3c90cc yesterday
 History
 2 contributors
@henrikboulund@tboulund
76 lines (70 sloc)  1.89 KB

pipeline{
    agent any
    triggers
    {
        pollSCM("* * * * *")
    }

    stages{
        stage("STARTUP")
        {
            steps{
                dir("Tests")
                {
                    sh "rm -rf TestResults"
                }
            }
        }
        stage("BUILD"){
            steps{

                sh "dotnet build CalculatorPipeline.sln"
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }

        stage("TEST")
        {
            steps
            {
                dir("Tests")
                {
                    sh "dotnet add package coverlet.collector"
                    sh "dotnet test --collect:'XPlat Code Coverage'"
                }
            }
            post
            {
                success
                {
                    archiveArtifacts "Tests/TestResults/*/coverage.cobertura.xml"
                    publishCoverage adapters: [istanbulCoberturaAdapter(path: 'Tests/TestResults/*/coverage.cobertura.xml', thresholds: [[failUnhealthy: true, thresholdTarget: 'Conditional', unhealthyThreshold: 80.0, unstableThreshold: 50.0]])], checksName: '', sourceFileResolver: sourceFiles('NEVER_STORE')
                }
            }
            
        }

        stage("DEPLOY")
        {
            steps{
                echo "DEPLOY!!!"
            }
            
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
Footer
© 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
CalculatorPipeline/Jenkinsfile at master · henrikboulund/CalculatorPipeline
