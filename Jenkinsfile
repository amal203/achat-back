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
		
		
		stage('UNIT Testing'){
		steps{
			sh'mvn test'
              
		  }
		}
		
		stage('Integration testing'){
		steps{
			sh'mvn verify -DskipUnitTests'
              
		  }
		}
		
		stage('Maven Build'){
		steps{
			sh'mvn clean install'
              
		  }
		}
		
		stage('SonarQube analysis') {
            agent any
            
            steps {
            script{
              withSonarQubeEnv('sonarserver') {
                sh 'mvn clean package sonar:sonar'
              }
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
		
		
		
		
		}
}