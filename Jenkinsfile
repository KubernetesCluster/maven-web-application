node{

   def mavenHome= tool name: "maven"
	echo "The branch name is : " ${env.BRANCH_NAME}
	echo "The job name is : " ${env.JON_NAME}
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
