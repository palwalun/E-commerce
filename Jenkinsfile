pipeline{
 agent any
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
   stage('Deploy to K8s'){
    steps{
	 sh 'kubectl apply -f deployment.yml'
	}
   }
  
  }




}