pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build Started...'
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp index.html /var/www/html/'
            }
        }

        stage('Verify') {
            steps {
                sh 'ls -l /var/www/html'
            }
        }
    }
}
