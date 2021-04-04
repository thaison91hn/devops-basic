pipeline {
    environment {
    name = 'nginx_demo'
    tag = 'build_nummber'
    img = '${name}+ ":${tag}"'
    latest = '${name}+ ":latest"'
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
                sh 'sudo docker build -t $img $registry:$tag .'
                sh 'sudo docker push $registry'
            }
        }  
    }
}
