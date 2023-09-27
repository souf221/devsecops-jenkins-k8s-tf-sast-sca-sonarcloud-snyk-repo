pipeline {
  agent any
  tools {
    maven 'Maven_3_5_2'
  }
  stages {
    stage('Compile and Run Sonar Analysis') {
      steps {
        sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=asmicroservicesspring -Dsonar.organization=asmicroservicesspring -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=0276789007c8d134a6a421133cc2b388420e33b8'
      }
    }
    stage('Run SCA Analysis Using Snyk') {
      steps {
        withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
          sh 'mvn snyk:test -fn'
        }
      }
    }
    stage('Build') {
      steps {
        withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
          script {
            app = docker.build("asg")
          }
        }
      }
    }
    stage('Push') {
      steps {
        script {
          docker.withRegistry('https://298334504632.dkr.ecr.eu-west-3.amazonaws.com/', 'ecr:eu-west-3:aws-credentials') {
            app.push("latest")
          }
        }
      }
    }
  }
}
 

