pipeline {
<<<<<<< HEAD
=======
<<<<<<< HEAD
>>>>>>> b497c43f539afcc0790479c7baeaea95c9c3effd
 
 agent any
 
 environment {
    PROJECT_ID = "mi-primer-jenkins-290214"
    CLUSTER_NAME = 'kube-demo'
    LOCATION = 'us-east1-d'
    CREDENTIALS_ID = 'mi-primer-jenkins-290214'
  }   
 stages {
     stage('Checkout SCM') {
      steps {
       checkout scm
      }
     }
    stage('Build package') {

        steps {
        echo "Cleaning and packing.."
         sh 'mvn clean package'
<<<<<<< HEAD
        }
    }
     stage('Test') {
      steps {
       echo "Testing.."
       sh 'mvn test'
      }
     }
     stage('Build and push Docker Image') {
      steps{
        script {
           //appimage = docker.build( "almitarosita/devops:${env.BUILD_ID}")
           //appimage = docker.build("gcr.io/vaulted-quarter-260801/devops:${env.BUILD_ID}")
           //docker.withRegistry("https://registry.hub.docker.com",'docker-hub-credentials') 
           //docker.withRegistry('https://gcr.io','gcr:gcr'){
           //   appimage.push("${env.BUILD_ID}")
           //}
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
    }
     stage('Test') {
      steps {
       echo "Testing.."
       sh 'mvn test'
      }
     }
     stage('Build and push Docker Image') {
      steps{
        script {
           //appimage = docker.build( "almitarosita/devops:${env.BUILD_ID}")
           //appimage = docker.build("gcr.io/vaulted-quarter-260801/devops:${env.BUILD_ID}")
           //docker.withRegistry("https://registry.hub.docker.com",'docker-hub-credentials') 
           //docker.withRegistry('https://gcr.io','gcr:gcr'){
           //   appimage.push("${env.BUILD_ID}")
           //}
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
			    kubernetesDeploy(configs:"deployment.yaml", kubeconfigId: "mi-primer-jenkins-290214")
                }
            }
        }
    }    
>>>>>>> 2b427ed125ab3d2b9382b724dbddea6cf269fd39
>>>>>>> b497c43f539afcc0790479c7baeaea95c9c3effd
}
