pipeline {
    agent any

    tools {
       go "1.24.1"
    }

    stages {
        stage('Unit test') {
            steps {
                sh 'go test ./...'
            }
        }
        stage('Build') {
            steps {
                sh "go version"
                sh "go build -o main main.go"
            }
        }
        stage('Build and Push Docker image') {
            steps {
                sh "docker build --tag ttl.sh/myapp:1h ."
                sh "docker push ttl.sh/myapp:1h"
            }
        }
        stage('Deploy') {
            steps {
                withKubeConfig([credentialsId: 'k8s', : 'https://k8s:6443']) {
                    sh 'kubectl apply -f pod.yaml'
                }
            }
        }
    }
}
