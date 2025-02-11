pipeline {
    agent any
    environment {
        VERCEL_TOKEN = credentials('token-vercel')  // Usar el ID que diste a las credenciales
        VERCEL_ORG_ID = 'c3AHu2AjRy6ljp2cnIMaTb1U'  // ID de la organización
        VERCEL_PROJECT_NAME = 'meinunezs-projects'   // Nombre de tu proyecto
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
                script {
                    echo 'Deploying to Vercel...'
                    sh """
                        vercel --token $VERCEL_TOKEN --prod --confirm --scope $VERCEL_ORG_ID --name $VERCEL_PROJECT_NAME
                    """
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
