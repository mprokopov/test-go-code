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
        stage('Build Docker image') {
            steps {
                sh "docker build --tag myapp:latest ."
            }
        }
        // stage('Deploy') {
        //     steps {
        //         withCredentials([sshUserPrivateKey(credentialsId: 'target-ssh-key', keyFileVariable: 'key', usernameVariable: 'username')]) {
        //             sh """
        //             ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook --inventory hosts.ini --private-key=${key} playbook.yml
        //             """
        //         }
        //     }
        // }
    }
}
