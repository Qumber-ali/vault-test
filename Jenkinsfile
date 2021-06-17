def secrets = [
  [path: 'secret/jenkins/github', engineVersion: 2, secretValues: [
    [envVar: 'PRIVATE_TOKEN', vaultKey: 'private-token'],
    [envVar: 'PUBLIC_TOKEN', vaultKey: 'public-token'],
    [envVar: 'API_KEY', vaultKey: 'api-key']]],
]
def configuration = [vaultUrl: 'http://172.17.0.10:8200',  vaultCredentialId: 'vault-approle', engineVersion: 2]
                      
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
      stage('Vault') {
        steps {
          withVault([configuration: configuration, vaultSecrets: secrets]) {
            sh "echo ${env.PRIVATE_TOKEN} > ${WORKSPACE}/test_variables.txt"
            sh "echo ${env.PUBLIC_TOKEN} >> ${WORKSPACE}/test_variables.txt"
            sh "echo ${env.API_KEY} >> ${WORKSPACE}/test_variables.txt"
          }
        }  
      }
    }
}
