pipeline {
<<<<<<< HEAD
 
 agent any
 
 environment {
=======
    agent any
    environment {
>>>>>>> 55a8fcbd01fc147f636fbce5cff20776fdcf420b
        PROJECT_ID = 'mi-primer-jenkins-290214'
        CLUSTER_NAME = 'kube-demo'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'mi-primer-jenkins-290214'
<<<<<<< HEAD
  }   
 stages {
     stage('Checkout SCM') {
      steps {
       checkout scm
      }
     }
    
    
     stage('Build and push Docker Image') {
      steps{
        script {
           //appimage = docker.build( "almitarosita/devops:${env.BUILD_ID}")
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
=======
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
                    myapp = docker.build("grissy/hello:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
        stage('Deploy to GKE') {
            steps{
                sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
                step([$class: 'KubernetesEngineBuilder', projectId: env.mi-primer-jenkins-290214, clusterName: env.kube-demo, location: env.us-central1-c, manifestPattern: 'deployment.yaml', credentialsId: env.mi-primer-jenkins-290214, verifyDeployments: true])
            }
        }
    }    
>>>>>>> 55a8fcbd01fc147f636fbce5cff20776fdcf420b
}
