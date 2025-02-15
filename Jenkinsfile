pipeline {
    agent any
    environment {
        VERCEL_ORG_ID = 'team_JRC3KLemWgxsnZfSW3832CZq'  // Team ID en Vercel
        VERCEL_PROJECT_NAME = 'meinunezs-projects'       // Nombre del proyecto en Vercel
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/meinunez/my-first-pipeline.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'vercel-token', variable: 'VERCEL_TOKEN')]) {
                    sh '''
                        export VERCEL_ORG_ID="team_JRC3KLemWgxsnZfSW3832CZq"
                        export VERCEL_PROJECT_NAME="meinunezs-projects"
                        vercel --token $VERCEL_TOKEN --prod --scope $VERCEL_ORG_ID
                    '''
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
