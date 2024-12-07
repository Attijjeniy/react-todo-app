pipeline {
    agent any
    stages {
        stage('Pull Code from Git') {
            steps {
                sh '''
                    echo "Checkout done"
                    # Replace the following with your Git checkout command
                    git clone https://your-repo-url.git /path/to/your/project
                    cd /path/to/your/project
                '''
            }
        }
        stage('Build') {
            steps {
                sh '''
                    npm install
                    npm run build
                    # Ensure the target directory exists before copying files
                    sudo mkdir -p /opt/development/react
                    sudo cp -r build/* /opt/development/react/
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    cd /opt/development/react
                    # Use pm2 serve for serving static files
                    pm2 serve /opt/development/react 3000 --name "react-to-do-app" --spa
                '''
            }
        }
    }
    post {
        always {
            sh 'pm2 list' // Check PM2 status after the pipeline
        }
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed. Check logs for details.'
        }
    }
}
