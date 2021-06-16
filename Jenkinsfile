node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/jglick/simple-maven-project-with-tests.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.      
      //comment
      mvnHome = tool 'MAVEN_HOME'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore "-DaltDeploymentRepository=nexus::default::http://13.126.195.192:8081/nexus/content/repositories/snapshots" clean deploy'
         } else {
           // bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore '-DaltDeploymentRepository=nexus::default::http://13.126.195.192:8081/nexus' clean deploy/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   stage('Sonar Analysis') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" sonar:sonar'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" sonar:sonar/)
         }
      }
   }
}
