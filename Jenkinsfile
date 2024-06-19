pipeline {
  agent any
  
   tools {nodejs "node"}
    
  stages {
    stage("GitHub git cloning") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/clement2019/Deploy-NodeAp-AWS-EKS-jenkins.git']])
                    //git branch: 'main', url: 'https://github.com/clement2019/Deploy-NodeAp-AWS-EKS-jenkins.git' 
                }
            }
        }
     
    stage('intialising npm installation.......') {
      steps {
        sh 'npm install'
      }
    }
  
     stage('Building Docker Image for the app') {
            steps {
                script {
                 
                  sh 'printenv'
                  sh 'git version'
                  //sh 'docker build -t good777lord/node-app:""$Build_ID"".'
                  sh 'docker build -t good777lord/node-app1 .'
                }
            }
        }


        stage('Deploying the Docker Image to DockerHub') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'gooddocker', variable: 'gooddocker')]) {
                    sh 'docker login -u good777lord -p ${gooddocker}'
            }
            //normally
            //sh 'docker push good777lord/node-app:""$Build_ID""'
            sh 'docker push good777lord/node-app1:latest'
        }
            }   
        }
         
     

  }
}
