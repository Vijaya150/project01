pipeline {
    agent any
    stages {
        stage('git cloned') {
            steps {
                git url: 'https://github.com/Vijaya150/project01/', branch: "master"
            }
        }
        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t vijayadarshini/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push vijayadarshini/staragileprojectfinance:v1'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21211 -p 8083:8081 vijayadarshini/staragileprojectfinance:v1'
            }
        }
    }
}
