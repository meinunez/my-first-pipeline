pipeline {
    agent any
    environment {
        VERCEL_ORG_ID = 'team_JRC3KLemWgxsnZfSW3832CZq'  // Team ID en Vercel
        VERCEL_PROJECT_ID = 'c3AHu2AjRy6ljp2cnIMaTb1U'   // ID del proyecto en Vercel
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
                        vercel --token $VERCEL_TOKEN --prod --scope $VERCEL_ORG_ID --project $VERCEL_PROJECT_ID
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
