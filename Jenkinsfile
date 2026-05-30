pipeline {
    agent any
    environment {
        SERVER = "ubuntu@13.222.133.136" 
        WEB_DIR = "/home/ubuntu/nginx-project"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Ninad262002/Static_website_jenkins.git
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
