node
{
def mavenHome= tool name: "maven3.6.3"

 stage('CheckOutCode')
 {
 git branch: 'development', credentialsId: '59b29e0a-0084-4ef5-b135-6230a9f6ab6c', url: 'https://github.com/tejkumaraws/maven-web-application.git'
 }
 stage('Build')
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 stage('ExecuteSonarQube')
 {
  sh "${mavenHome}/bin/mvn sonar:sonar"   
 }
 stage('UploadArtificartIntoNexus')
 {
  sh "${mavenHome}/bin/mvn deploy"   
 }
 stage('DeployApplicationTOmcat')
 {
  sshagent(['08d3184c-dce4-430d-a658-ca411cbc462b'])
  {
   sh  "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.94.210.62:/opt/apache-tomcat-9.0.31/webapps/"
}   
 }
 stage('SendEmail')
 {
     emailext body: '''Build is over


Regards,
Tej.''', subject: 'Build is Successful', to: 'tejkumaraws@gmail.com'
 }
}
