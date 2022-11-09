pipeline{
agent any
	stages{
		
		  stage('Git Checkout'){
		steps{
            echo ('Getting project from git');
            git branch:'main',
        
            url:'https://github.com/amal203/achat-back.git'
		  }
		}
		
		
		stage('Unit Testing'){
		steps{
			sh'mvn test'
              
		  }
		}
		
		stage('Integration Testing'){
		steps{
			sh'mvn verify -DskipUnitTests'
              
		  }
		}
		
		stage('Maven Build'){
		steps{
			sh'mvn clean install'
              
		  }
		}
		
		
		
		
		}
}