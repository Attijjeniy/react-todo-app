pipeline {
    agent any
    stages {
        stage('Pull Code from Git') {
            steps {
                sh 'echo "Checkout done"'
            }
        }
        stage('Build') {
            steps {
                sh '''
                    npm install
                    npm run build
                    sudo mkdir -p /opt/development/react
                    sudo cp -r build/* /opt/development/react/
                    sudo chown -R jenkins:jenkins /opt/development/react
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    pm2 delete react-to-do-app || true
                    pm2 serve /opt/development/react 3000 --name "react-to-do-app" --spa
                '''
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed. Check PM2 logs for details.'
            sh 'pm2 logs react-to-do-app'
        }
    }
}
