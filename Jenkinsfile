def gv

pipeline {   
    agent any
    tools {
        maven 'maven-3.9.16' // Specify the Maven version to use
    }
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run tests after build')
    }

  stages {
        stage("init") {
            steps {
               script {
                    gv = load "script.groovy"
                } 
            }
        }
        stage("build") {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }

        stage("test") {
            when {
                expression { 
                    params.executeTests 
                    }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    env.ENV input message: "Select the environment to deploy to", ok: "Yes, deploy", parameters: [choice(name: 'APP_ENV1', choices: ['dev', 'staging', 'production'], description: 'Select the environment to deploy to')]

                    gv.deployApp()
                    echo "Deploying to environment: ${ENV}"
                }
            }
        }               
    }
} 
