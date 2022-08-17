node {

    def mvnHome
    def tomcat = 'C:\\Tomcat'
    def PAT
    
    withCredentials([string(credentialsId: 'GH-PAT', variable: 'GHPAT')]) {
    
        PAT = "$GHPAT"
        bat("echo $PAT")
    }

    stage('Checkout') { // for display purposes
      // Get some code from a GitHub repository
      git "https://$PAT@github.com/abhishekd07/VulnerableLab.git"
      // Get the Maven Home.
 
      mvnHome = tool name: '3.8.6', type: 'maven'
   }
   
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean deploy/)
         }
      }
   }
   
   stage('Download Artifact') {
      // Run the curl command to download the war file from GitHub Package Registry
      bat("curl -O -L https://$PAT@maven.pkg.github.com/abhishekd07/VulnerableLab/org/cysecurity/javavulnerablelab/6.0.0/javavulnerablelab-6.0.0.war")
      
   }
   
   stage('Deploy to Tomcat Server') {
      bat "copy javavulnerablelab-6.0.0.war C:\\Tomcat\\webapps\\javavulnerablelab-6.0.0.war"
   }
   
}
