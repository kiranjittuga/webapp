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
		     sh 'wget "https://raw.githubusercontent.com/kiranjittuga/webapp/master/owasp-dependency-check.sh" '
		     sh 'chmod +x owasp-dependency-check.sh'
		     sh 'bash owasp-dependency-check.sh'
		     sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
            }
    }
	  stage ('SAST') {
		steps {
		withSonarQubeEnv('sonar') {
			sh 'mvn sonar:sonar'
			sh 'cat target/sonar/report-task.txt'
		       }
		}
	}
  
    
   
   
    stage ('Build') {
      steps {
       sh 'mvn clean package'
      }
      
    }
	
  }
} 
    
    
    
    
    
 
    
