  pipeline{
 agent any
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
   
   stage('Nexus-Deployment'){
      steps{
	  sh "mvn deploy"
	  }
   }
   
   stage('App Deployment In Tomcat server'){
      steps{
      sshagent(['371d53fd-9138-4744-8b32-632aa6d86081']) {
          sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-cicd-pipeline-project/target/maven-web-application.war ec2-user@18.118.8.38:/opt/tomcat/webapps"
	   
           }
	  }
   }
   
   
   
 
 } // closing the stages
 }// closing pipeline
