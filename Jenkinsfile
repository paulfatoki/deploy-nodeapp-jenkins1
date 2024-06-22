pipeline {
  agent any
  
   tools {nodejs "node"}
    
  stages {
    stage("GitHub git cloning") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/paulfatoki/deploy-nodeapp-jenkins1.git']])
                    //git branch: 'main', url: 'https://github.com/paulfatoki/deploy-nodeapp-jenkins1.git' 
                }
            }
        }
     
    stage('connecting npm installation.......') {
      steps {
        sh 'npm install'
      }
    }
  
     stage('Docker build initializing') {
            steps {
                script {
                 
                  sh 'printenv'
                  sh 'git version'
                  //sh 'docker build -t paulfatoki/node-app:""$Build_ID"".'
                  sh 'docker build -t paulfatoki/node-app1 .'
                }
            }
        }


        stage('Connecting the Docker Image to DockerHub') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'dockerhub_ID', variable: 'dockerhub_ID')]) {
                    sh 'docker login -u paulfatoki -p ${dockerhub_ID}'
            }
  
            //sh 'docker push paulfatoki/node-app:""$Build_ID""'
            sh 'docker push paulfatoki/node-app1:latest'
        }
            }   
        }
         
     

  }
}
