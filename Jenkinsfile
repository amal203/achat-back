pipeline{
agent:any
	stages{
		stage('MVN COMPILE'){
		steps{
			sh'mvn compile'
			}
		  }
		  stage('MVN CLEAN'){
		steps{
			sh'mvn clean'
			}
		  }
		  stage('Git Checkout'){
		steps{
            echo ('Getting project from git');
            git branch:'main',
        
            url:'https://github.com/amal203/achat-back.git'
		  }
		
		
		
		
		
		}
}