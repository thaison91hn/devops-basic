pipeline {
    agent {label:'Docker-agent'}
    stages {
        stage('clone') {
            steps {
                git 'https://github.com/thaison91hn/devops-basic.git'
            }
        }
        stage('build dockerfile') {
            steps {
                sh 'docker build -t test_nginx .'
            }
        }  
    }
}
