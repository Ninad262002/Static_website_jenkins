pipeline {
    agent any
    environment {
        SERVER = "ubuntu@NGINX_SERVER_IP"
        WEB_DIR = "/var/www/html"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'YOUR_REPO_URL'
            }
        }
        stage('List Files') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    scp -r * ${SERVER}:/tmp/
                    ssh ${SERVER} "sudo rm -rf ${WEB_DIR}/* && sudo cp -r /tmp/* ${WEB_DIR}/ && sudo systemctl restart nginx"
                """
            }
        }
    }
    post {
        success {
            echo "Deployment Completed"
        }
        failure {
            echo "Deployment Failed"
        }
    }
}
