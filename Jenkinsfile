pipeline {
    
    agent any
    environment {
        // FOO will be available in entire pipeline
        FOO = "PIPELINE"
    }
    
    stages {

        stage("API Testing") {
            steps {
                bat 'C:/Users/Stephan/AppData/Roaming/npm/newman run C:/SW/newman/TEST_API.json -r htmlextra'
            }
        }
        
        stage("Publish") {
            parallel {
                stage('Pre-Release') {
                    when { expression { !params.RELEASE } }
                    steps {
                        echo 'sdsd'
                    }
                }
                stage("Release") {
                    when { expression { params.RELEASE } }
                    steps {
                        echo 'sdsd'
                    }
                }
            }
        }

        stage("Deploy") {
            parallel {
                stage("INT") {
                    when { expression { params.DEPLOY_TO == "INT" } }
                    steps {
                        echo 'sdsd'
                        

                    }
                }
                stage("PRE") {
                    when { expression { params.DEPLOY_TO == "PRE" } }
                    steps {
                        echo 'sdsd'
                        

                    }
                }
                stage("PROD") {
                    when { expression { params.DEPLOY_TO == "PROD" } }
                    environment {
                        // BAR will only be available in this stage
                        BAR = "STAGE"
                    }
                    steps {
                        echo 'sdsd'
                        echo "FOO is $FOO and BAR is $BAR"
                    }
                }
            }
        }
    }
    post {
        always {            echo 'This will always run'        }
        success {            echo 'This will run only if successful'        }
        failure {            echo 'This will run only if failed'        }
        unstable {            echo 'This will run only if the run was marked as unstable'        }
        changed {            echo 'This will run only if the state of the Pipeline has changed. eg if the Pipeline was previously failing but is now successful'        }
    }
}
