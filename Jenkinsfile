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
                    sh """
                              mkdir -p ~/.ssh
          ssh-keyscan -H target >> ~/.ssh/known_hosts
"""
    sh 'scp -i ${key} main ${username}@target:~'
    sh 'scp -i ${key} main.service ${username}@target:~'
}

                sh '''
                ssh -i ${key} ${username}@target -C "sudo mv main.service /etc/systemd/system/;sudo systemctl start main;systemctl status main"
                '''
            }
        }
    }
}
