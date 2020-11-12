pipeline {
    agent any
    tools { 
        maven 'mvn' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
		    export M2_HOME=/usr/share/maven
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
	     stage ('Check-Git-Secrets') {
		    steps {
	        sh 'rm trufflehog || true'
		sh 'docker pull gesellix/trufflehog'
		sh 'docker run -t gesellix/trufflehog --json https://github.com/AliElKhatteb/webapp.git > trufflehog'
		sh 'cat trufflehog'
	    }
	    }
	    
	  stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
	stage ('Deploy') {
            steps {
                sh 'cp target/*.war /opt/tomcat/webapps'
            }
        }
	 stage ('Source-Composition-Analysis') {
		steps {
		     sh 'rm owasp-* || true'
		    // sh 'wget https://github.com/AliElKhatteb/webapp/blob/dev/owasp-dependency-check.sh'	
		     sh 'chmod +x owasp-dependency-check.sh'
		     sh 'bash owasp-dependency-check.sh'
		     sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
		}
	}
	    
	 
	       
	    
	
    }
}
