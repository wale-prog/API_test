pipeline {
    agent any
    tools {
        nodejs 'node20' // Ensure you have a NodeJS tool configured in Jenkins
    }

    options {
      skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout Code') {
            steps {
                cleanWs()
                echo 'Checking out code...'
                checkout scm
                echo 'Cloned from GitHub repository:'
            }
                
        }
        stage('Install dependencies') {
            steps {
               sh '''
                    which npm
                    npm install
                    npm install -g newman
                '''
                echo 'Dependencies installed successfully.'
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
            junit 'results/junit-result.xml'
        }
        //success {
           // echo 'This will run only if the pipeline succeeds.'
        //}
        failure {
            echo 'Pipeline failed.'
        }
    }
}