pipeline {
  agent any

  environment {
	scannerHome = tool 'sonar'
  }
  tools{
  	jdk 'JDK17'
  	maven 'MAVEN3'
  }
  stages {	
	stage('Maven Compile'){
		steps{
			echo 'Project compile stage'
			sh 'mvn compile'
	       	}
	}
	
	stage('Unit Test') {
	   steps {
			echo 'Project Testing stage'
			sh 'mvn package'
	       
       		}
   	}

	stage('Jacoco Coverage Report') {
        	steps{
            		jacoco()
		}
	}       
       
      stage('Sonarqube') {
  steps {
    script {
			 withSonarQubeEnv('sonar') {
				 sh ''' ${scannerHome}/bin/sonar-scanner \
				 -Dsonar.poject.Key=spring-test \
				 -Dsonar.projectName=spring-test '''
			 }
		 }
  }
}	
	
			
    
  }
}
