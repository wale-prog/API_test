pipeline {
    agent any

    options {
      skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout Code') {
            steps {
                cleanWs()
                echo 'Checking out code...'
                checkout scm
            }
                
        }
        stage('Install dependencies') {
            steps {
               sh '''
                    echo 'Installing dependencies...'
                    npm install
                    npm install -g newman
                '''
            }
        }
        stage('Run tests with Newman') {
            steps {
                echo 'Running Tests...'
                sh'''
                    npm test
                '''
            }
        }
    }

    post {
        always {
            junit 'results/junit-report.xml'
        }
        success {
           // echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}