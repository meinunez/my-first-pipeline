pipeline {
    agent any
    environment {
        // Cargar el token desde las credenciales de Jenkins
        VERCEL_TOKEN = credentials('token-vercel')  // Usando la credencial de token en Jenkins
        VERCEL_ORG_ID = 'team_JRC3KLemWgxsnZfSW3832CZq'  // ID de tu equipo en Vercel
        VERCEL_PROJECT_NAME = 'meinunezs-projects'  // Nombre de tu proyecto en Vercel
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
                    withCredentials([string(credentialsId: 'token-vercel', variable: 'VERCEL_TOKEN')]) {
                        sh """
                            vercel --token $VERCEL_TOKEN --prod --yes --scope $VERCEL_ORG_ID --name $VERCEL_PROJECT_NAME
                        """
                    }
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
