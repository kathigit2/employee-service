pipeline {

  agent any
  tools { 
        maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh 'docker build -t employee-service .'
      }
    }   
    stage('push image to DockerHub'){
      steps {
         withDockerRegistry(credentialsId: 'docker-hub', url: 'https://index.docker.io/v1/') {
         sh 'docker tag ramdev/dev:employee-service'
         sh 'docker push ramdev/dev:employee-service'  
         }
      }
    }
   }
