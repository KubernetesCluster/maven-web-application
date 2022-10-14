 pipeline{
 
 tools{
 maven "maven"
 }
 
 stages{
 
   stage('CodeCheckOut'){
   steps{
   git branch: 'jenkins-descriptive', credentialsId: 'fbd0e2e3-4f82-4812-83f6-61edb7b5fdb0', url: 'https://github.com/KubernetesCluster/maven-web-application.git'
   }
   }
   
   stage('Build'){
     steps{
	 sh "mvn clean package"
	 }
   }
   
   stage('Sonar Report'){
      steps{
	  sh "mvn sonar:sonar"
	  }
   }
   
   
   
   
 
 } // closing the stages
 }// closing pipeline
