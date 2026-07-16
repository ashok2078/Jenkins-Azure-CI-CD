pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build Started...'
            }
        }

        stage('Backup') {
            steps {
                sh '''
                sudo mkdir -p /var/www/html/backup
                sudo cp /var/www/html/index.html /var/www/html/backup/index-$(date +%F-%H-%M-%S).html
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                sudo cp index.html /var/www/html/
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                ls -l /var/www/html
                ls -l /var/www/html/backup
                '''
            }
        }
    }
}
