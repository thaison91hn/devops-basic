pipeline {
    agent any
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        }
        stage('build dockerfile') {
            steps {
                withDockerRegistry(url:'https://hub.docker.com/') {
                    sh 'docker build -t thaison91hp/devops-basic:v1 .'
                    sh 'docker push thaison91hp/devops-basic:v1'
                }
            }
        }  
    }
}
