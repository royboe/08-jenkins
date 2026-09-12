dev gv

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
        stage("init") {
            steps {
               script {
                    gv = load.script('script.groovy')
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
                    gv.buildApp()
                }
            }
        }
        
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }               
    }
} 
