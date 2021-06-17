def secrets = [
  [path: 'secret/jenkins/github', engineVersion: 2, secretValues: [
    [envVar: 'PRIVATE_TOKEN', vaultKey: 'private-token'],
    [envVar: 'PUBLIC_TOKEN', vaultKey: 'public-token'],
    [envVar: 'API_KEY', vaultKey: 'api-key']]],
]
def configuration = [vaultUrl: 'http://172.19.0.2:8200',  vaultCredentialId: 'vault-approle', engineVersion: 2]
                      
pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
        disableConcurrentBuilds()
    }
    stages{   
      stage('Vault') {
        steps {
          withVault([configuration: configuration, vaultSecrets: secrets]) {
            sh "echo ${env.PRIVATE_TOKEN} > /home/ec2-user/test_variables.txt"
            sh "echo ${env.PUBLIC_TOKEN} >> /home/ec2-user/test_variables.txt"
            sh "echo ${env.API_KEY} >> /home/ec2-user/test_variables.txt"
          }
        }  
      }
    }
}
