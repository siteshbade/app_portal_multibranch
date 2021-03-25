
pipeline{

	agent any
	
	environment{
	 mvnHome= tool('M3')
	 def tomcatWeb = 'http://3.141.164.2:8085///opt//tomcat//webapps'
	 def tomcatBin = 'http://3.141.164.2:8085//opt//tomcat//bin'
	 def tomcatStatus = ''
	 
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
		sh "${tomcatBin}\\shutdown.sh"
                 sleep(time:10,unit:"SECONDS")
               
				}
    }
   stage('Deploy to Production'){
   
		steps{
     		 "cp target\\nvnshoppingcart.war /"${tomcatWeb}//nvnshoppingcart.war/""
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
