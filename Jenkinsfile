pipeline {
    agent any
    environment {
        // Cargar el token desde las credenciales de Jenkins
        VERCEL_TOKEN = credentials('vercel-token')  // Usando la credencial de token en Jenkins
        VERCEL_ORG_ID = 'team_JRC3KLemWgxsnZfSW3832CZq'  // ID de tu equipo en Vercel
        VERCEL_PROJECT_NAME = 'meinunezs-projects'  // Nombre de tu proyecto en Vercel
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
                    sh """
                        vercel --token $VERCEL_TOKEN --prod --yes --scope $VERCEL_ORG_ID --name $VERCEL_PROJECT_NAME
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
