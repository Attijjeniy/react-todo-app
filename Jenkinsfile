pipeline {
    agent any
    stages {
        stage('Pull Code from Git') {
            steps {
                sh 'echo "Checkout done"'
                // Add your Git checkout command here if needed
            }
        }
        stage('Build') {
            steps {
                sh '''
                    npm install
                    npm run build
                    cp -r build/* /opt/development/react
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    cd /opt/development/react
                    pm2 start /opt/development/react --name "react-to-do-app" --port 3000 --force
                '''
            }
        }
    }
}
