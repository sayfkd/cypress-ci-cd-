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
                sh 'npx cypress run'
            }
        }
    }

    post{
        always {
            archiveArtifacts artifacts: 'cypress/reports/**/*.*', followSymlinks: false
        }
    }
}