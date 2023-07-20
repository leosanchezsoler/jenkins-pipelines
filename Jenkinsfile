pipeline {
    agent any
    parameters {
        choice(name: "VERSION", choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: "executeTests", defaultValue: true, description: '')
    }
    tools {
        maven 'Maven'
    }
    environment {
        NEW_VERSION = "1.3.0"
    }

    stages {
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'dev'
                }
            }
            steps {
                echo "building the application..."
                echo "building version ${NEW_VERSION}"
                sh "mvn install"
            }
        }
        stage("test") {
            when {
                expression {
                    params.executeTests
                }
            }
            steps{
                echo "testing the application..."
                echo "deploying version ${params.VERSION}"

            }
        }
        stage("deploy") {

            steps{
                echo "deploying the application..."
            }
        }
    }
    post {
        always {
            // This will be always executed, no matter if the steps avobe failed or not
            echo "always executed"
        }
        success {
            // Run if it succeeds
            echo "only executed on success"
        }
        failure {
            // Run if it fails
            echo "only executed on failure"
        }
    }
}