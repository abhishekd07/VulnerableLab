node {
   def mvnHome
   stage('Checkout') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/abhishekd07/VulnerableLab.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool name: 'mvn_3_6_3', type: 'maven'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   
stage('Selenium Test') {
	bat 'C:\\Checkmarx\\Installers\\CxIAST\\WebDrivers_Selenium\\Selenium.jar'
}

stage('CxIAST') {
step([$class: 'CxIASTBuilder', appIp: 'localhost', appName: 'JavaVulnerableLab', appPort: 8360, password: '{AQAAABAAAAAQYtajilBHWA+LE+iE00upYpqlBLMWFj0WVeqnaMREXdI=}', scanTag: 'Build_Number:$BUILD_NUMBER', serverUrl: 'http://localhost:8380/', username: 'abhishek'])
}


}
