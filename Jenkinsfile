pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myapp .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker rm -f test-myapp 2>/dev/null || true'
                sh 'docker run -d --name test-myapp -p 5001:5000 myapp'
                sh 'docker stop test-myapp'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop myapp 2>/dev/null || true'
                sh 'docker rm myapp 2>/dev/null || true'
                sh 'docker run -d --name myapp -p 5000:5000 myapp'
            }
        }
    }
}
