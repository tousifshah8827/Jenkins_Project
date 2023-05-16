pipeline {
    agent any
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
        }
   }
