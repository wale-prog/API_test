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
                echo 'Cloned from GitHub repository:'
            }
                
        }
        stage('Install dependencies') {
            steps {
                echo 'Installing dependencies...'
                // Ensure Node.js and npm are installed on the Jenkins agent
               sh '''
                    echo 'Installing dependencies...'
                    npm install
                    npm install -g newman
                '''
            }
            echo 'Dependencies installed successfully.'
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