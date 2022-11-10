pipeline{
 agent any

    tools {
        maven 'M2_HOME'
       
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "0.0.0.0:8081"
        NEXUS_REPOSITORY = "maven-nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
      
    }

	stages{
		
		  stage('Git Checkout'){
		steps{
            echo ('Getting project from git');
            git branch:'main',
        
            url:'https://github.com/amal203/achat-back.git'
		  }
		}
		
		  stage('Cleaning the project') {
            steps{
                sh 'mvn clean'
            }

        }
          stage ('Artifact construction') {
            steps{
                sh 'mvn  package'
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
		
		
		
		stage('SonarQube analysis') {
            agent any
            
            steps {
            script{
              withSonarQubeEnv(credentialsId:'sonar-api') {
                sh 'mvn clean package sonar:sonar'
              }
              }
            }
          }
         
		 stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
		
		
		
		}
		
		
}