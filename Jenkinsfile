pipeline {
    agent {
        docker {
            image "cypress/browsers"
            args '--entrypoint=""'
        }
    }

    parameters {
        string(name: 'TAG', defaultValue: '@login', description: 'Tag des tests Cypress')
    }

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
                  //  sh "npx cypress run --reporter junit --env grepTags='${params.TAG}'"
                   sh "npx cypress run --reporter junit"
                }
            }
        }
    }

    post {
        always {
            echo "Archivage des rapports Cypress"
            junit 'results/**/*.xml'
            //archiveArtifacts artifacts: 'cypress/reports/**/*.*', followSymlinks: false
        }
    }
}
