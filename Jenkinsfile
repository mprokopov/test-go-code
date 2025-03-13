pipeline {
    agent any

    // tools {
    //    go "go"
    // }

    stages {
        stage('Build') {
            steps {
                sh "go version"
                sh "go build -o main main.go"
            }
        }
    }
}
