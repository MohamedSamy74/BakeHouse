pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                sh '''
                kubectl get pod
                '''
            }
        }
        stage('test') {
            steps {
                echo 'test'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
            }
        }
    }
}
