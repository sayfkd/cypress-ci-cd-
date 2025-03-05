pipeline {
    agent {
        docker {
            image "cypress/browsers"
            args '--entrypoint=""'
        }
    }

    parameters {
        choice(name: 'TAG', choices: ['smoke', 'e2e', 'sanity', 'regression', 'login'], description: 'TAG')
        string(name: 'NAME', defaultValue: '', description: 'Nom du test ')
    }    }

    stages {
        stage('Vérifier la version de npm') {
            steps {
                sh "npm -v"
                sh "npm ci"
            }
        }
        stage('Test Cypress') {
            steps {
                 script {
                    def testCommand = "npx cypress run --reporter junit"
                    --env grep="auth user"
                    if (params.TEST_NAME?.trim()) {
                        testCommand += " --env grep='${params.TEST_NAME}'"
                    } else {
                        testCommand += " --env grepTags='@${params.TEST_TYPE}'"
                    }
                    sh testCommand
                }
            }
        }
        stage('Test Cypress') {
            steps {
                script {
                   sh "npx cypress run --reporter junit"
                }
            }
        }
    }

    post {
        always {
            // echo "Archivage des rapports Cypress"
            junit 'results/**/*.xml'
            //archiveArtifacts artifacts: 'cypress/reports/**/*.*', followSymlinks: false
        }
    }
}

