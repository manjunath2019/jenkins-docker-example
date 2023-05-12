pipeline{
    agent any
    tools {
        maven 'M2-HOME'
    }
    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/manjunath2019/jenkins-docker-example.git']])
                sh "mvn clean package"
            }
        }
        stage ('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t first-image .'
                }
            }
        }
        stage ('Push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'manjunathdocker', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u manjunathdocker -p ${dockerhubpwd}'
                    sh 'docker tag first-image manjunathdocker/first-image'
                    sh 'docker push manjunathdocker/first-image'
                    }
                }
            }
        }    
    }
}
