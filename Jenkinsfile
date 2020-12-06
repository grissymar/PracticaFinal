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
        stage('Deploy to Kubernetes') {
            steps {
              echo "Deploying to Kubernetes Cluster.."
              sh 'ls -ltr'
              sh 'pwd'
              sh "sed -i 's/tagversion/${env.BUILD_ID}/g' deployment.yaml"
              step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
              echo "Deployment to Kubernetes cluster completed.."
      }
     }
    }
}
