pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio
                git url: 'https://github.com/meinunez/my-first-pipeline.git',  branch: 'main' 
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
                // Ejecutar pruebas
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                // Lógica de despliegue (por ejemplo, subir a un proveedor de la nube)
                echo 'Deploying application...'
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
