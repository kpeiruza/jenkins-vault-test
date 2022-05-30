def secrets = [
  [path: 'kv/jenkins/demo', engineVersion: 2, secretValues: [
    [envVar: 'PRIVATE_TOKEN', vaultKey: 'PRIVATE_TOKEN'],
    [envVar: 'PUBLIC_TOKEN', vaultKey: 'PUBLIC_TOKEN'],
    [envVar: 'API_KEY', vaultKey: 'API_KEY']]],
]

def configuration = [vaultUrl: 'http://vault.vault.svc.cluster.local:8200',  vaultCredentialId: 'bfbac4b3-f814-4700-9a4c-5531abeb4752', engineVersion: 2]
                      
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
            sh "echo ${env.PRIVATE_TOKEN}"
            sh "echo ${env.PUBLIC_TOKEN}"
            sh "echo ${env.API_KEY}"
          }
        }  
      }
    }
}
