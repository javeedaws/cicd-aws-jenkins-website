pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/javeedaws/cicd-aws-jenkins-website.git'
        BRANCH = 'awsproject'
        DEPLOY_DIR = '/var/www/html'
    }

    stages {
        stage('Pull Code from GitHub') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                sudo rm -rf /var/www/html/*
                sudo cp -r * ${DEPLOY_DIR}/
                '''
            }
        }

        stage('Restart Apache') {
            steps {
                sh '''
                sudo systemctl restart httpd
                sudo systemctl status httpd | head -n 5
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful 🎉'
        }
        failure {
            echo 'Deployment failed ❌'
        }
    }
}
