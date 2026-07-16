pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build Started...'
            }
        }

        stage('Code Validation') {
            steps {
                sh 'tidy -errors -q index.html'
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
                sh 'sudo cp index.html /var/www/html/'
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                echo "Checking website health..."
                curl -f http://localhost > /dev/null
                '''
            }
        }
    }

    post {
        failure {
            sh '''
            echo "Deployment Failed! Starting Rollback..."

            sudo cp $(ls -t /var/www/html/backup/index-*.html | head -1) /var/www/html/index.html

            echo "Rollback Completed Successfully!"
            '''
        }
    }
}
