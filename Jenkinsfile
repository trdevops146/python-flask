pipeline {
    agent any
    stages{
        stage('Checkout the code stage'){
            steps{
                git branch: 'main', url: 'https://github.com/trdevops146/python-flask.git'
            }
        }
        stage('Update the packages on the jenkins Agent'){
            steps{
                sh '''
                sudo apt update
                '''
            }
        }
        stage('Containerize the application'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        docker build -t trdevops/python-app:${BUILD_NUMBER} .
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push trdevops/python-app:${BUILD_NUMBER}
                        sudo chmod a+x docker.sh
                        docker.sh
                        docker container run -it --name p1 -d trdevops/python-app:${BUILD_NUMBER}
                    '''
                }

            }
        }
    }
}