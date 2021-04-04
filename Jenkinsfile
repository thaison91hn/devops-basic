pipeline {
    environment {
    name = 'nginx_demo'
    img = '${name}'
    registry = 'thaison91hp/devops-basic'
    }
    parameters {
    string(name:'DEPLOY_TAG', defaultValue:'dev-0.0.1')
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
                    echo "Building docker image $img:$DEPLOY_TAG"
                    sh 'docker build -t $img:$DEPLOY_TAG .'
                    echo "push image to dockerhub"
                    sh 'docker push $registry:$DEPLOY_TAG'
                }
            }
        }  
    }
}
