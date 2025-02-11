pipeline {
    agent any

    environment {
        // Definir variables de entorno necesarias para el despliegue
        VERCEL_TOKEN = 'rXxjscfyXm4ZlmKgcOUiU4no'   // Token de Vercel
        VERCEL_ORG_ID = 'tu-id-de-organizacion'      // ID de tu organización en Vercel
        VERCEL_PROJECT_NAME = 'meinunezs-projects'    // Nombre del proyecto en Vercel
    }

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde GitHub
                git url: 'https://github.com/meinunez/my-first-pipeline.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Instalar dependencias
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Ejecutar pruebas del proyecto
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Despliegue automático a Vercel usando la CLI de Vercel
                    echo 'Deploying to Vercel...'

                    // Despliegue usando el comando Vercel CLI
                    sh """
                        vercel --token $VERCEL_TOKEN --prod --confirm --scope $VERCEL_ORG_ID --name $VERCEL_PROJECT_NAME
                    """
                }
            }
        }
    }

    post {
        always {
            // Este bloque siempre se ejecutará al final del pipeline
            echo 'Pipeline completed.'
        }
        failure {
            // Este bloque se ejecutará si el pipeline falla
            echo 'Pipeline failed!'
        }
    }
}
