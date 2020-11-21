node
{

   def mvnHome = tool name: 'maven_3.6.3' , type: 'maven'
  
 stage('Checkout')
 {
 	git credentialsId: 'test_maven_Project', url: 'https://github.com/nareshdara/maven-web-application-1.git'
 
 }
 
 stage('Build')
 {
 sh  "${mvnHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSoanrQubeReport')
 {
 sh  "${mvnHome}/bin/mvn sonar:sonar"
 }
 
 stage('UploadArtifactintoNexus')
 {
 sh  "${mvnHome}/bin/mvn deploy"
 }
 
 stage('DeployAppintoTomcat')
 {
 sshagent(['maven_pipeline_project1']) {
   
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.95.121:/opt/apache-tomcat-9.0.40/webapps/"
 }
 }
 stage('SendEmailNotification')
 {
emailext body: '''Test webapp project

regards,
Naresh''', subject: 'Test webapp project', to: 'nareshdara200@gmail.com'
 }
}
