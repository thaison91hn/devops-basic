pipeline {
    environment {
    NAME = 'nginx_demo'
    REGISTRY = 'thaison91hp/devops-basic'
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
                withDockerRegistry(credentialsId: 'c0fd71ad-9253-4118-ac13-bbb6a349a0d1', url: 'https://index.docker.io/v1/') {
                    echo "Building docker image $NAME:$BUILD_NUMBER"
                    sh 'docker build -t $NAME:$BUILD_NUMBER .'
                    sh 'docker tag $NAME:$BUILD_NUMBER $REGISTRY:$BUILD_NUMBER
                    echo "push image to dockerhub"
                    sh 'docker push $REGISTRY:$BUILD_NUMBER'
                }
            }
        }  
    }
}
