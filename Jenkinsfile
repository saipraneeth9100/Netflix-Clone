pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/netflix-clone"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Deployment Directory') {
            steps {
                sh '''
                sudo mkdir -p $DEPLOY_DIR
                '''
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh '''
                sudo rsync -av --delete ./ $DEPLOY_DIR/
                '''
            }
        }

        stage('Set Permissions') {
            steps {
                sh '''
                sudo chown -R www-data:www-data $DEPLOY_DIR
                sudo chmod -R 755 $DEPLOY_DIR
                '''
            }
        }

        stage('Restart Nginx') {
            steps {
                sh '''
                sudo systemctl restart nginx
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment SUCCESS 🚀 Netflix Clone is live'
        }
        failure {
            echo 'Deployment FAILED ❌ Check logs'
        }
    }
}
