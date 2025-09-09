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
                sh '''
                    python3 --version
                    sudo apt update
                    sudo apt install -y python3-pip python3-venv
                    pip3 install build
                    python3 -m build
                '''
            }
        }
    }
}
