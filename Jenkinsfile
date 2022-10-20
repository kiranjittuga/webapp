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
			sh 'wget https://raw.githubusercontent.com/kiranjittuga/webapp/master/dojo_ci_cd.py'
			sh 'chmod +x dojo_ci_cd.py'
      sh 'python3 dojo_ci_cd.py --product=1 --file "/tests/scans/Bodgeit-burp.xml" --scanner="Burp Scan" --high=0 --host=http://localhost:8000 --api_key=<1222c567c6b54b30ef9d6f8a2f867e2a3f850406> --user=admin'  
       
        }
     }    
  }
} 
    
    
    
    
    
 
    
