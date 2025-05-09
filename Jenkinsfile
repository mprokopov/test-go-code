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
                withCredentials([sshUserPrivateKey(credentialsId: 'target-ssh-key', keyFileVariable: 'key', usernameVariable: 'username')]) {
                    sh """
ssh -i $key -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null ${username}@docker -C 'docker run --detach --publish 4444:4444 ttl.sh/myapp:1h'
                    """
                }
            }
        }
    }
}
