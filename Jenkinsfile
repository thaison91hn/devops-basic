pipeline {
    agent { label 'Docker-agent'}
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        }
        stage('build dockerfile') {
            steps {
                sh 'sudo docker build -t test_nginx .'
                sh 'sudo docker run -d test_nginx'
            }
        }  
    }
}
