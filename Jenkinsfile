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
	    
	  stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }    
	    
	 
	       
	    
	
    }
}
