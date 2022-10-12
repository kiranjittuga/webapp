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
        sh 'docker run gesellix/trufflehog https://github.com/kiranjittuga/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    } 
    
  
    
   
   
    stage ('Build') {
      steps {
       sh 'mvn clean package'
      }
      
    }
	  
        stage ('Upload Reports to Defect Dojo') {
		    steps {
			sh 'pip install requests'
			sh 'wget https://raw.githubusercontent.com/kiranjittuga/webapp/master/upload-results.py'
			sh 'chmod +x upload-results.py'
      sh 'python upload-results.py --host 127.0.0.1:8000 --api_key 1cfb69d0577faa22a07f810444cd3bdf41ac8fe4 --engagement_id 1 --result_file trufflehog --username admin --scanner "SSL Labs Scan"'    
      
        }
     }    
  }
} 
    
    
    
    
    
 
    
