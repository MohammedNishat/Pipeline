node{

   def tomcatWeb = '/home/ec2-user/tomcat/webapps'
   def tomcatBin = '/home/ec2-user/tomcat/bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/PuthaSathish/deploy_jenkinsfile_to_server.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'local_maven', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\JenkinsWar.war \"${tomcatWeb}\\JenkinsWar.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}
