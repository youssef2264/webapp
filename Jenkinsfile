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
	    
	 
	       
	    
	
    }
}
