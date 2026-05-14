pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                echo 'Repository already checked out'
            }
        }

        stage('Deploy to Nginx') {
            steps {
                sh '''
                sudo mkdir -p /var/www/netflix-clone
                sudo rm -rf /var/www/netflix-clone/*
                sudo cp -r * /var/www/netflix-clone/
                '''
            }
        }

        stage('Restart Nginx') {
            steps {
                sh 'sudo systemctl restart nginx'
            }
        }

    }
}
