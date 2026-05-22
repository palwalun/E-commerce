pipeline{
 agent any
  stages{
   stage('Checkout'){
    steps{
        git url: 'https://github.com/palwalun/E-commerce.git',
	    branch: 'master'
    }
   }
   stage {
    steps{
	 sh 'mvn clean package -Dskiptests'
	}
   }
  
  }




}