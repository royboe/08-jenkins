pipeline {   
    agent any
    tools {
        maven 'maven-3.9.16' // Specify the Maven version to use
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0', '1.5.9'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run tests after build')
    }

  stages {

        stage("test") {
            steps {
                script {
                    echo "Testing the application..."
                    echo "Executing pipeline on branch: ${BRANCH_NAME}"
                }
            }
        }

        stage("build") {
            when {
                expression { 
                    BRANCH_NAME == 'main'
                 }
            }
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }

        stage("deploy") {
            when {
                expression { 
                    BRANCH_NAME == 'main'
                 }
            }
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }               
    }
} 
