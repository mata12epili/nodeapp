pipeline {
    agent any

    environment {
        DEPLOY_DIR = '/www/var/html'
        SERVICE_NAME = 'nginx'

    }
    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'

                echo 'Building the application...'
                sh 'npm run build'
                echo 'Build completed successfully.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying build to local server...'
                // Add test steps here
                sh '''
                echo "Copying build files to $DEPLOY_DIR..."
                sudo rm -rf ${DEPLOY_DIR}/*
                sudo cp -r dist/* ${DEPLOY_DIR}/

                echo "Restarting $SERVICE_NAME"
                sudo systemctl restart ${SERVICE_NAME}

                '''
                echo 'Deployment completed successfully.'
            }
        }
    }
}