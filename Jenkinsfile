pipeline {
    agent any
    stages {
        stage('Build Docker Image for DEV') {
            when {
                branch 'dev'
            }            
            steps {
                script {
                    def app = docker.build("latest")
                    docker.withRegistry('https://registry.hub.docker.com/vivekmore5292/dev', 'Docker') {
                    app.push()
                    }
                }
            }
        }
        stage('Build Docker Image for QA') {
            when {
                branch 'qa'
            }            
            steps {
                script {
                    def app = docker.build("vivekmore/qa:latest")
                    docker.withRegistry('https://registry.hub.docker.com/vivekmore5292/qa', 'Docker') {
                        app.push()
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up...'
            deleteDir()
        }
    }
}
