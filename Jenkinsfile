pipeline {
    environment {
    NAME = 'nginx_demo'
    REGISTRY = 'thaison91hp/devops-basic'
    }
    parameters {
    string(name:'DEPLOY_TAG',defaultValue: 'dev-0.0.1')
    }    
    agent { label 'Docker-slave'}

    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        }
        stage('build dockerfile') {
            steps {
                withDockerRegistry(credentialsId: 'c0fd71ad-9253-4118-ac13-bbb6a349a0d1', url: 'https://index.docker.io/v1/') { 
                    echo "Building docker image $NAME:$DEPLOY_TAG"
                    sh 'docker build -t $NAME:$DEPLOY_TAG .'
                    sh 'docker tag $NAME:$DEPLOY_TAG $REGISTRY:$DEPLOY_TAG'
                    echo "push image to dockerhub"
                    sh 'docker push $REGISTRY:$DEPLOY_TAG'
                }
            }
        }
        stage('pull & run docker image') {
            steps {
                echo "remove image if exits"
                sh 'docker rmi -f $REGISTRY:$DEPLOY_TAG' 
                echo "pull image from $REGISTRY & run image"
                sh 'docker pull $REGISTRY:$DEPLOY_TAG'
                sh 'docker run -d -p 8080:80 $REGISTRY:$DEPLOY_TAG'
            }
        }  
    }
}
