node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/AliElKhatteb/jenkins_maven_testing.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.
      mvnHome = tool 'M3'
      dep_check= tool 'vuln'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }

   stage ('sonarqube analysis'){
       bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore verify sonar:sonar/)
      }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   stage("Dependency Check") {

      bat(/"${dep_check}\bin\dependency-check" -f XML -s target\*.jar /)
      dependencyCheckPublisher pattern: 'dependency-check-report.xml'

      archiveArtifacts allowEmptyArchive: true, artifacts: 'dependency-check-report.xml', onlyIfSuccessful: true
    }

}
