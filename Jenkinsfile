
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
	  
	   
	 
   
   stage('Deploy to Production'){
   
		steps{
			sshagent(['jenkins-secret-text']) {

        sh "scp -o StrictHostKeyChecking=no webapp/target/nvnshoppingcart.war /opt/tomcat/webapps/"
    
		}
     	
	 }
   }
      stage ('Start Tomcat Server') {
	  steps{
         sleep(time:5,unit:"SECONDS") 
         sh "${tomcatBin}/startup.sh"
         sleep(time:100,unit:"SECONDS")
		 }
   }
	
	
	
	}
   
}
