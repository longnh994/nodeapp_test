pipeline {

    environment {
        dockerimagename = "longnh994/nodeapp:build-${env.BUILD_NUMBER}"
        dockerImage = ""
    }

    agent any

    stages {
        stage('Print env') {
            environment {
                A = credentials('testcre')
                B = credentials('testcre_USR')
                C = credentials('testcre_PSW')
            }
            steps {
                echo '$A'
                echo "$A"
                echo '$B'
                echo "$B"
            }
        }

        stage('Checkout Source') {
            steps {
                git 'https://github.com/longnh994/nodeapp_test'
            }
        }

        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build dockerimagename
                }
            }
        }

        stage('Push image') {
            environment {
                registryCredential = 'dockerhublogin'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com/', registryCredential) {
                    dockerImage.push()
                    }
                }
            }
        }

        // stage('Deploy') {
        //     steps {
        //         kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        //     }
        // }
    }
}