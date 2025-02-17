pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/meinunez/my-first-pipeline.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
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
                    sh 'vercel --token $VERCEL_TOKEN --prod --yes'
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
