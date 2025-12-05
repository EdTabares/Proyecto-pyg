pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *')
    }
    
    stages {
        stage('Descargar Código') {
            steps {
                echo '📥 Descargando código desde GitHub...'
                checkout scm
            }
        }
        
        stage('Ejecutar Pruebas') {
            steps {
                echo '🧪 Ejecutando pruebas...'
                bat 'npm test'
            }
        }
        
        stage('Resultado') {
            steps {
                echo '✅ Todo salió bien!'
            }
        }
    }
    
    post {
        success {
            echo '🎉 ¡Éxito! El código está perfecto'
        }
        failure {
            echo '❌ Error: Algo salió mal'
        }
    }
}