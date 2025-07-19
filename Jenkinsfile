pipeline {
    agent any

    environment {
        EC2_HOST= '13.201.131.164' 
        SSH_CREDENTIAL_ID= 'jenkinsmaster'
        REMOTE_USER= 'Ubuntu'
        REMOTE_PATH= '/home/ubuntu/app'
        WEB_ROOT= '/var/www/html' // Replace with your EC2 instance ID

    }
    stages {
        stage('Build') {
            steps {
                echo 'Installing dependencies...'
                ssh 'npm install'

                echo 'Building the application...'
                ssh 'npm run build'
                echo 'Build completed successfully.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to EC2 at' + env.EC2_HOST
                ssh"""
                echo " Creating remote directory"
                ssh -o StrictHostKeyChecking=no  ${REMOTE_USER}@${EC2_HOST} "mkdir -p ${REMOTE_PATH}"
                
                echo "Copying files to remote EC2 ..."
                ssh -o StrictHostKeyChecking=no -r dist/* ${REMOTE_USER}@${EC2_HOST} :${REMOTE_PATH}/
                echo "Moving files to web root and restarting nginx"
                sudo rm -rf ${WEB_ROOT}/*
                sudo cp -r dist/* ${REMOTE_PATH}/* ${WEB_ROOT}/
                sudo systemctl restart nginx

                """
                echo 'Deployment completed successfully.'
            }
        }
    }
}