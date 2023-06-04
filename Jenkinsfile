pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    environment {	
	    DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	} 
stages{
    stage('Checkout from Github') {
      steps{
         script{
             checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'Github-Login1', url: 'https://github.com/suvo7886/Jenkins_Project_StarAgile.git']])
         }
           }
       }
      stage('Compile with Maven') {
       steps{
           bat 'mvn clean compile'
              }
            }
       stage('Test with Maven') {
       steps{
           bat 'mvn clean test'
              }
            }
       stage('Package with Maven') {
        steps{
           bat 'mvn clean package'
              }
            }
       stage("Docker Build"){
        steps {
			bat 'docker version'
			bat "docker build -t cicd-project:${BUILD_NUMBER} ."
			bat 'docker image list'
			bat "docker tag cicd-project:${BUILD_NUMBER} suvo7886/cicd-project:latest"
            }
        }
	   stage('Login to DockerHub') {
		steps {
		   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		   // bat 'winpty docker login'
			}
		}
       stage('Approve for Push Image to Dockerhub'){
        steps{
            script {
                env.APPROVED_DEPLOY = input message: 'User input required Choose "Yes" | "Abort"'
                }
            }
        }
	   stage('Push to DockerHub') {
		steps {
			bat "docker push suvo7886/cicd-project:latest"
			}
		}
       stage('Deploy to Tomcat Server') {
        steps{
           script{
             sshPublisher(publishers: [sshPublisherDesc(configName: 'Tomcat', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\webapps\\addressbook.war', remoteDirectorySDF: false, removePrefix: 'workspace\\CICD\\target\\', sourceFiles: 'workspace\\CICD\\target\\addressbook.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
           }
         }
      }
   }
}
