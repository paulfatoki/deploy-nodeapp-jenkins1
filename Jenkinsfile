pipeline {
  agent any
  
   tools {nodejs "node"}
    
  stages {
    stage("GitHub git cloning") {
            steps {
                script {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GITHUB_CREDENTIALS', url: 'https://github.com/clement2019/Deploy-NodeAp-AWS-EKS-jenkins.git']])
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
                  sh 'docker build -t good777lord/node-app:""$Build_ID"".'
                }
            }
        }


        stage('Deploying the Docker Image to DockerHub') {
            steps {
                script {
                 withCredentials([string(credentialsId: 'devopshintdocker', variable: 'devopshintdocker')]) {
                    sh 'docker login -u good777lord -p ${devopshintdocker}'
            }
            
            sh 'docker push good777lord/node-app:""$Build_ID""'
        }
            }   
        }
         
     stage('Kubernetes deployment of application') {
      steps {
        script {
          sh ('aws eks update-kubeconfig --name eks-cluster-100 --region eu-west-2')
          sh "kubectl get ns"
          sh "kubectl apply -f deployment.yaml"
        }
      }
    }

  }
}
