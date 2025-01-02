pipeline {
    agent any
 
    environment {
       PYTHON_PATH = 'C:\\Users\\thirishaa\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\thirishaa\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
       SONAR_SCANNER_PATH='C:\Program Files\sonar-scanner-6.2.1.4610-windows-x64\bin' 
    }
 
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Build') {
            steps {
                // Set the PATH and install dependencies using pip
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
                pip install -r requirement.txt
                '''
            }
        }
 
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonarqube-token') // Accessing the SonarQube token stored in Jenkins credentials
            }
            steps {
                bat '''
                set PATH=%PYTHON_PATH%;%PATH%
                sonar-scanner -Dsonar.projectKey=pipeline_trial1 ^
                  -Dsonar.sources=. ^
                  -Dsonar.host.url=http://localhost:9000 ^
                  -Dsonar.token=sqp_592cd6f9fa3bb339b08d5c2086d816c741c7f568
                '''
            }
        }
    }
 
    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            echo 'This runs regardless of the result.'
        }
    }
}
