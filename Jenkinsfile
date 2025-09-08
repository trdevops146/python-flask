pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout source code into workspace/python-project-1/
                git branch: 'main', url: 'https://github.com/trdevops146/python-flask.git'
            }
        }
        stage('Build') {
            steps {
                sh 'ls -la'
                sh 'python3 --version'
            }
        }
    }
}
