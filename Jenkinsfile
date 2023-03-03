pipeline {
    agent any 

    //define variables for later use
    //for predefined ones use 'http://10.176.129.14:8080/env-vars.html/'
    environment {
        NEW_VERSION = '1.0'
    }
    
    stages {
        stage("build") {
            //print and use of variable (for ${} use " instead of ')
            echo "building version ... ${NEW_VERSION}" 
            //do stuff
        }

        
        stage("test") {
            when {
                //when condition to execute on a condition
                expression{ 
                    params.executeTests //same as params.executeTest == True
                }
            }
            echo 'testing... '
            //do stuff
        }
    
        stage("deploy") {
            when { 
                expression {
                    BRANCH_NAME == 'dev'
                    //boolean expression
                }
            }
            echo 'deploying... '
            //do stuff
        }
    }

    post {
        always {
            //actions that always happen after pipeline
        }
        
        success {
            //do stuff if pipeline was successfull
        }

        failure {
            //do stuff on failure
        }
    }
}
