// defining that groovy files can be used globally in the pipeline
def gv

pipeline {
    agent any
    parameters {
        string(name: 'Requester', defaultValue: 'Tech lead', description: 'Who asked you to run this?')
		choice(name: 'Version', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'Execute Tests', defaultValue: true, description: "Choose whether you'd like to execute tests or not")
    }
    stages {
        stage("init") {
            steps {
                script {
                   gv = load "magic_stages.groovy" 
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
                    gv.deployApp()
                }
            }
        }
    }   
}