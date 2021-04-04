pipeline {
    environment {
    name = 'nginx_demo'
    img = '${name}'
    registry = 'thaison91hp/devops-basic'
    registryCredential = 'thaison91hp'
    }
    agent { label 'Docker-agent'}
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        }
        stage('build dockerfile') {
            steps {
                sh 'sudo -s'
                withDockerRegistry(credentialsId: 'c0fd71ad-9253-4118-ac13-bbb6a349a0d1', url: 'https://index.docker.io/') {
                sh 'sudo docker build -t $registry:$BUILD_NUMBER .'
                sh 'sudo docker push $registry'
                }
            }
        }  
    }
}
