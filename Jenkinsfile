pipeline {
    agent any
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        stage('build dockerfile') {
            steps {
                withDockerRegistry(credentialsld:'c0fd71ad-9253-4118-ac13-bbb6a349a0d1',url:'https://index.docker.io/v1/'){
                    sh label:'', script: 'docker build -t thaison91hp/devops-basic:v1 .'
                    sh label:'', script: 'docker push thaison91hp/devops-basic:v1'
                }
            }
        }
    }
}
