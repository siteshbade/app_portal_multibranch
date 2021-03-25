
pipeline{

	agent any
	
	environment{
	 mvnHome= tool('M3')
	def tomcatWeb = '/opt/tomcat/webapps'
	def tomcatBin = '/opt/tomcat/bin'
	//def tomcatStatus = ''
	 
	}
	

	stages{
	
	   stage('SCM Checkout'){
		steps{
		 git 'https://github.com/siteshbade/app_portal_multibranch.git'
		 }
   }
   stage('Compile-Package-create-war-file'){
		steps{
      // Get maven home path
        
      sh "  ${mvnHome} -Dmaven.test.failure.ignore  package"
		}
      }
	  
	   
	 
   stage ('Stop Tomcat Server') {
		steps{
		//sshagent(['Tomcat-cred'])
		//sh " ${tomcatBin}/shutdown.sh"
		sh "systemctl stop tomcat"
                 sleep(time:10,unit:"SECONDS")
			}
               
				
    }
   stage('Deploy to Production'){
   
		steps{
			deploy adapters: [tomcat8(path: '', url: 'http://3.141.164.2:8085/')], contextPath: '/var/lib/jenkins/workspace/mvn build 1/targetnvnshoppingcart.war', onFailure: false, war: 'war'
     	
	 }
   }
      stage ('Start Tomcat Server') {
	  steps{
         sleep(time:5,unit:"SECONDS") 
         sh "${tomcatBin}\\startup.sh"
         sleep(time:100,unit:"SECONDS")
		 }
   }
	
	
	
	}
   
}
