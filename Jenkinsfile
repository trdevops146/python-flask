pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout source code into workspace/python-project-1/
                git branch: 'main', url: 'https://github.com/trdevops146/python-flask.git'
            }
        }
        stage('Update the packages') {
            steps {
                sh '''
                    sudo apt update
                '''
            }
        }
        stage('Build the application as a docker image'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        sudo docker build -t trdevops/python-app:${env.BUILD_NUMBER} .
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        sudo docker push trdevops/python-app:${env.BUILD_NUMBER}
                        sudo docker rm -f python-app || true
                        sudo docker run -d --name python-app -p 5000:5000 trdevops/python-app:${env.BUILD_NUMBER}
                    """
                }
            }
        }
    }
}
