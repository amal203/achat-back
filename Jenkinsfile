pipeline{
agent any
tools{
		maven 'Maven 4.0.0'
		}
	stages{
		
		  stage('Git Checkout'){
		steps{
            echo ('Getting project from git');
            git branch:'main',
        
            url:'https://github.com/amal203/achat-back.git'
		  }
		}
		
		
		stage('UNIT Testing'){
		steps{
			sh'mvn test'
              
		  }
		}
		
		
		
		
		
		
		}
}