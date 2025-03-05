pipeline{
    agent{
        docker{
            image "cypress/included"
            args '--entrypoint=""'
        }
    }
    stages{
        stage('verifier la version de npm'){
            steps{
                sh "npm -v"
                   }
        }
        stage('test cypress'){
            steps{
                sh 'npx cypress run'
            }
        }
    }
}