pipeline {
    agent any
    environment {
        PROJECT_ID = 'mi-primer-jenkins-290214'
        CLUSTER_NAME = 'kube-demo'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'mi-primer-jenkins-290214'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry("") {
                            dockerImage.push()
                    }
                }
            }
        }        
        stage('Deploy to GKE') {
            steps{
			  script{
			    kubernetesDeploy(configs:deployment.yaml", kubeconfigId: mi-primer-jenkins-290214, verifyDeployments: true])}
                
            }
        }
    }    
}
