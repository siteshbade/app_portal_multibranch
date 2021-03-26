
pipeline{

	agent any
	
	environment{
	 mvnHome= tool('M3')
	 
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
    deploy adapters: [tomcat8(credentialsId: 'tomcate', path: '', url: 'http://3.143.116.80:8085/')], contextPath: 'nvnshoppingcart', onFailure: false, war: 'target\\*.war'
	 }
   }
      
	
	
	
	}
   
}

