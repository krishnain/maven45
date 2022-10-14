node('built-in') 
{
   stage('ContinuousDownload') 
   { 
       git 'https://github.com/krishnain/maven45.git'
   }
   stage('ContinuousBuild')
   {
       sh 'mvn package'
   }
   stage('ContinuousDeployment')
   {
       deploy adapters: [tomcat9(credentialsId: '836c40e4-0e18-42ae-a5dc-72108054bd9b', path: '', url: 'http://172.31.24.16:8080')], contextPath: 'testapp', war: '**/*.war'
   }
   stage('ContinuousTesting')
   {
       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh 'java -jar /home/ubuntu/.jenkins/workspace/ScriptedPipeline1/testing.jar'
   }
   stage('ContinuousDelivery')
   {
       deploy adapters: [tomcat9(credentialsId: '836c40e4-0e18-42ae-a5dc-72108054bd9b', path: '', url: 'http://172.31.21.0:8080')], contextPath: 'prodapp', war: '**/*.war'
   }
   
   
   
   
   
   
}
