node('built-in') 
{
   stage('ContinuousDownload') 
   { 
      try
      {
           git 'https://github.com/krishnain/maven45.git'
      }
      catch(Exception e1)
      {
         mail bcc: '', body: 'Jenkins is unable to download the java code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
         exit(1)
      }
   }
   stage('ContinuousBuild')
   {
      try
      {
          sh 'mvn package'
      }
      catch(Exception e2)
      {
         mail bcc: '', body: 'Jenkins is unable to create artifact', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.team@gmail.com'
         exit(1)
      }
      
   }
   stage('ContinuousDeployment')
   {
      try
      {
         deploy adapters: [tomcat9(credentialsId: '836c40e4-0e18-42ae-a5dc-72108054bd9b', path: '', url: 'http://172.31.24.16:8080')], contextPath: 'testapp', war: '**/*.war'
      }
      catch(Exception e3)
      {
          mail bcc: '', body: 'Jenkins is unable to deploy to tomcat on qaserver', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
         exit(1)
      }
   }
   stage('ContinuousTesting')
   {
      try
      {
       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline1/testing.jar'
      }
      catch(Exception e4)
      {
         mail bcc: '', body: 'Selenium scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'testing.team@gmail.com'
         exit(1)
      }
   }
   stage('ContinuousDelivery')
   {
      try
      {
          deploy adapters: [tomcat9(credentialsId: '836c40e4-0e18-42ae-a5dc-72108054bd9b', path: '', url: 'http://172.31.21.0:8080')], contextPath: 'prodapp', war: '**/*.war'
      }
      catch(Exception e5)
      {
         mail bcc: '', body: 'Unable to deploy into tomcat on prodservers', cc: '', from: '', replyTo: '', subject: '', to: 'delivery.team@gmail.com'
         
      }
   }
   
   
   
   
   
   
}
