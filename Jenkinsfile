pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'testing/master']], userRemoteConfigs: [[url: 'git@github.com:Kartik-777/react.git']]])
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['3.110.182.244']) {
                    sh 'scp -r ./build ec2-user@3.110.182.244:/var/www/html/reactproject'
                    sshCommand remoteUser: 'ec2-user', remoteHost: '3.110.182.244', command: 'cd /var/www/html/reactproject && npm install && npm start'
                }
            }
        }
    }
}
