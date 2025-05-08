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
        stage('Deploy') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'target-ssh-key', keyFileVariable: 'key', usernameVariable: 'username')]) {
    sh 'scp main ${username}@target:~ -i ${key}'
}
                
            }
        }
    }
}
