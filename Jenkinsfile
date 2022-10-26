node 
{
   def mavenHome = tool name: "maven3.8.6"
    stage('CheckoutCode')
    {
        git branch:'master', credentialsId: 'b4414d6c-2b7e-4137-aa15-9d1ebeeee955', url: 'https://github.com/devipriyak22/maven-web-application.git'
    }
    stage('build')
    {
       sh "${mavenHome}/bin/mvn clean package"
    }
    stage('execute sonar')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
   stage('nexus')
   {
       sh "${mavenHome}/bin/mvn deploy"
   }
   stage('tomcat')
   {
     
       
       sshagent(['00713220-0c0a-4206-bb2d-6cf113c9bf7a']) 
  
       {
           sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.93.3:/opt/apache-tomcat-9.0.67/webapps/"
    }
   }
}



