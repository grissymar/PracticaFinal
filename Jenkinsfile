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
                    myapp = docker.build("grissy/hello:${env.hello-world}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    appimage = docker.build("gcr.io/vaulted-quarter-260801/devops:${env.BUILD_ID}")
           	    //docker.withRegistry("https://registry.hub.docker.com",'docker-hub-credentials') 
                   docker.withRegistry('https://gcr.io','gcr:gcr'){
                   appimage.push("${env.BUILD_ID}")
		 }
                }
            }
        }        
        stage('Deploy to GKE') {
            steps{
                sh "sed -i 's/hello:latest/hello:${env.hello-world}/g' deployment.yaml"
                step([$class: 'KubernetesEngineBuilder', projectId: env.mi-primer-jenkins-290214, clusterName: env.kube-demo, location: env.us-central1-c, manifestPattern: 'deployment.yaml', credentialsId: env.mi-primer-jenkins-290214, verifyDeployments: true])
            }
        }
    }    
}
