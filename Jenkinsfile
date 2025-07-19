pipeline {
    agent any
    stages {
        stage("Build") {
            steps {
                echo "start building"
                sh "npm install"
                sh "npm run build"
                echo "building completed"
            }
        }
        stage("Deploy") {
            steps {
                echo "start deploying on ec2"
                sh "scp -r -o strictCheckingOfKey=No ./dist/* /home/ubuntu/Node-app/"
                sh "npm start"
                echo "Deploying completed"
            }
        }
        }
    }
