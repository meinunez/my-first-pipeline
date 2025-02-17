
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/meinunez/my-first-pipeline.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // Instalar las dependencias necesarias
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'  // Esto genera el directorio 'build' o 'dist'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'  // Ejecutar las pruebas si es necesario
            }
        }

        stage('Deploy to Vercel') {
            steps {
                withCredentials([string(credentialsId: 'vercel-token', variable: 'VERCEL_TOKEN')]) {
                    sh 'vercel --token $VERCEL_TOKEN --prod --yes'  // Desplegar en Vercel
                }
            }
        }
    }

    post {
        always {
            echo '¡Despliegue automatizado en Vercel!'
        }
        failure {
            echo '¡El despliegue automatizado en Vercel ha fallado!'
        }
    }
}
