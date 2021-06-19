
// def hey = groovy.json.JsonOutput.toJson(list)
                      
pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
        disableConcurrentBuilds()
    }
    stages{   
      stage('Create File') {
        steps{
          sh "touch ${WORKSPACE}/test_variables.txt"
        }
      }
        stage('Creating Groovy List from Map'){
          steps{
		  sh "/root/.sdkman/candidates/groovy/2.3.6/bin/groovy /root/.sdkman/test >> /root/.sdkman/out.txt"
          }
        }
      
}

}
