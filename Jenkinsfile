
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
			deploy adapters: [tomcat8(credentialsId: 'Tomcat-cred', path: '', url: 'http://3.142.69.80:8085/')], contextPath: '/opt/tomcat/webapps/', onFailure: false, war: 'target\\*war'
     	
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
