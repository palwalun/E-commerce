pipeline{
 agent any
 environment{
  ACR_LOGIN_SERVER = 'devopsproject2.azurecr.io'
  IMAGE_NAME = 'e-comm'
  TAG = 'latest'
  }
  stages{
   stage('Checkout'){
    steps{
        git url: 'https://github.com/palwalun/E-commerce.git',
	    branch: 'master'
    }
   }
   stage('Build stage'){
    steps{
	 sh 'mvn clean package -DskipTests'
	}
   }
   stage('Build Image'){
    steps{
	 sh 'docker build -t e-comm .'
	}
   }
   stage('Login to ACR') {
       steps {
         withCredentials([usernamePassword(
             credentialsId: 'acr-creds',
             usernameVariable: 'ACR_USERNAME',
             passwordVariable: 'ACR_PASSWORD'
         )]) {
             sh "echo \$ACR_PASSWORD | docker login \$ACR_LOGIN_SERVER -u \$ACR_USERNAME --password-stdin"
           }
          }
         }
		 
	stage('Tag Image') {
        steps {
         sh '''
           docker tag ${IMAGE_NAME}:${TAG} \
           $ACR_LOGIN_SERVER/${IMAGE_NAME}:${TAG}
         '''
          }
        }
    stage('Push Image to ACR'){
	      steps{
	        sh 'docker push $ACR_LOGIN_SERVER/${IMAGE_NAME}:${TAG}'
	    }
	   }
	stage('Deploy to k8s'){
	      steps{
	        sh 'kubectl apply -f deployment.yml'
	    }
	   }
   
  
  }




}