pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
	
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Check-Git-Secrets'){
      steps {
        sh 'rm trufflehog || true'
        sh 'sudo docker run gesellix/trufflehog https://github.com/kiranjittuga/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    } 
    
	  stage ('Source-Composition-Analysis') {
		steps {
		     sh 'rm owasp-* || true'
		     sh 'wget https://raw.githubusercontent.com/kiranjittuga/webapp/master/owasp-dependency-check.sh'
            }
    }
  
    
   
   
    stage ('Build') {
      steps {
       sh 'mvn clean package'
      }
      
    }
	
  }
} 
    
    
    
    
    
 
    
