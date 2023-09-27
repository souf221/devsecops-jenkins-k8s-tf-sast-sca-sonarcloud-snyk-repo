pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=asmicroservicesspring -Dsonar.organization=asmicroservicesspring -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=0276789007c8d134a6a421133cc2b388420e33b8'
			}
        } 
  }
}
