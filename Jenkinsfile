pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
stages{
    stage('checkout the project from Github') {
      steps{
         git 'https://github.com/devopscbabu/DevOpsAddressBook.git'
           }
       }
      stage('compile maven project') {
       steps{
           sh 'mvn clean compile'
              }
            }
       stage('Test maven project') {
       steps{
           sh 'mvn clean test'
              }
            }
       stage('Package maven project') {
       steps{
           sh 'mvn clean package'
              }
            }
        }
   }
