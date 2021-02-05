node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/youssef2264/webapp.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }

  stage ('Deploy-To-Tomcat') {
            bat "copy 'target\\WebApp.war' E:\\apache-tomcat-9.0.43\\webapps\\webapp.war"
           }
   stage('Results') {
      archiveArtifacts 'target/*.war'
   }

}
