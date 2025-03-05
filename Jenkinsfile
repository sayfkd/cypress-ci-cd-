pipeline{
    agent{
        docker{
            image "cypress/browsers"
            args '--entrypoint=""'
        }
    }

    parameters {
        string(name: 'TAG', defaultValue: '@login', description: 'Tag')
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
                sh 'npx cypress run --env grepTags=${params.TAG}'
            }
        }
    }

    post{
        always {
            archiveArtifacts artifacts: 'cypress/reports/**/*.*', followSymlinks: false
        }
    }
}