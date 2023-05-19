pipeline {
    agent {
      label 'slave1'
      }
    tools{
        maven 'M2_HOME'
    }
stages{
    stage('Checkout from Github') {
      steps{
         git 'https://github.com/suvo7886/Jenkins_Project_StarAgile.git'
           }
       }
      stage('Compile with Maven') {
       steps{
           sh 'mvn clean compile'
              }
            }
       stage('Test with Maven') {
       steps{
           sh 'mvn clean test'
              }
            }
       stage('Package with Maven') {
       steps{
           sh 'mvn clean package'
              }
            }
       stage('Deploy to Prod Server') {
       steps{
           script{
           sshPublisher(publishers: [sshPublisherDesc(configName: 'Tomcat_Server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/opt/tomcat/webapps/addressbook.war', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/addressbook.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
           }
         }
      }
   }
}
