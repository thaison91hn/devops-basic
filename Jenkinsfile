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
                withDockerRegistry(credentialsId:'d042ad57-c098-430e-be65-922a7a422a10', url: 'https://index.docker.io/v1/') { 
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
                sh 'docker rm $(docker ps -all -q)"
                echo "pull image from $REGISTRY & run image"
                sh 'docker pull $REGISTRY:$DEPLOY_TAG'
                sh 'docker run --name $NAME -d -p 8083:80 $REGISTRY:$DEPLOY_TAG'
            }
        }  
    }

    post {
        success {

             echo 'send email to devopsadmin'
                 mail to: 'sondv@vps.com.vn',
                      subject: "failed pipeline",
                      body: "test email toi sondv"
	}
    }
}       
