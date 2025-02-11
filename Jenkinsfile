pipeline {
    agent any
    environment {
        VERCEL_PROJECT_ID = 'c3AHu2AjRy6ljp2cnIMaTb1U'  // ID del proyecto en Vercel
        VERCEL_TOKEN = credentials('vercel-token')  // Usando las credenciales de Jenkins para el token
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([string(credentialsId: 'vercel-token', variable: 'VERCEL_TOKEN')]) {
                    // Despliegue con el token de Vercel
                    sh '''
                        vercel --token $VERCEL_TOKEN --prod --project-id $VERCEL_PROJECT_ID
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
