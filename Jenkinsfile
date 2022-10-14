/*pipeline{

agent any

tools{
maven 'maven3.8.2'

}

triggers{
pollSCM('* * * * *')
}

options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
}

stages{

  stage('CheckOutCode'){
    steps{
    git branch: 'development', credentialsId: '957b543e-6f77-4cef-9aec-82e9b0230975', url: 'https://github.com/devopstrainingblr/maven-web-application-1.git'
	
	}
  }
  
  stage('Build'){
  steps{
  sh  "mvn clean package"
  }
  }
/*
 stage('ExecuteSonarQubeReport'){
  steps{
  sh  "mvn clean sonar:sonar"
  }
  }
  
  stage('UploadArtifactsIntoNexus'){
  steps{
  sh  "mvn clean deploy"
  }
  }
  
  stage('DeployAppIntoTomcat'){
  steps{
  sshagent(['bfe1b3c1-c29b-4a4d-b97a-c068b7748cd0']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.190.162:/opt/apache-tomcat-9.0.50/webapps/"    
  }
  }
  }
  */
}//Stages Closing

/* post{

 success{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
 failure{
 emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
          subject: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          body: "Pipeline Build is over .. Build # is ..${env.BUILD_NUMBER} and Build status is.. ${currentBuild.result}.",
          replyTo: 'devopstrainingblr@gmail.com'
 }
 
}


}//Pipeline closing

*/




// Prabesh written
// Scripted
node{

   def mavenHome= tool name: "maven"

// Checkout the git code
 stage('CodeCheckout'){
  git branch: 'jenkin-scripted', credentialsId: 'fbd0e2e3-4f82-4812-83f6-61edb7b5fdb0', url: 'https://github.com/KubernetesCluster/maven-web-application.git'
 
 }
 
 // Build the war
 stage('build'){
 
  sh "$mavenHome/bin/mvn clean package"
 }
 
 // Sonar report
  stage('SonarReport'){
   
   sh "$mavenHome/bin/mvn sonar:sonar"
  
  }
  
  // Nexus artifactory deploy
   stage('Nexus artifactory deploy'){
   
    sh "$mavenHome/bin/mvn deploy"
  
   }
   
   // application Deploy in apache tomcat server
   
   stage('Tomcat Application Deploy'){
   
   sshagent(['371d53fd-9138-4744-8b32-632aa6d86081']) {
       sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/maven-cicd-pipeline-project/target/maven-web-application.war ec2-user@18.118.8.38:/opt/tomcat/webapps"
	   
        }
  }

}










