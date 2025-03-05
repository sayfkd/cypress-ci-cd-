pipeline{
    agent{
        docker{
            image "cypress/browsers"
            args '--entrypoint=""'
        }
    }
    stages{
        stage('verifier la version de npm'){
            steps{
                sh "npm -v"
                sh "npm ci"

                   }
        }
        stage('test cypress'){
            steps{
                sh 'npx cypress run  --reporter cypress-mochawesome-reporter'
            }
        }
    }

    post{
        always {
            archiveArtifacts artifacts: 'cypress/reports/html/index.html', followSymlinks: false
        }
    }
}