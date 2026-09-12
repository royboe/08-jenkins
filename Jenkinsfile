pipeline {   
    agent any
    tools {
        maven 'maven-3.9.16' // Specify the Maven version to use
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run tests after build')
    }
    environment {
        // Define environment variables here
        APP_ENV = 'production'
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }

  stages {
        stage("build") {
            steps {
                echo 'building the application...'
                echo "Building version: ${NEW_VERSION} in environment: ${APP_ENV}"
            }
        }

        stage("test") {
            when {
                expression { 
                    params.executeTests 
                    }
            }
            steps {
                echo 'testing the application...'
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application...'
                echo "Deploying version: ${VERSION} in environment: ${APP_ENV}"
                withCredentials([usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) 
            }
        }               
    }
} 
