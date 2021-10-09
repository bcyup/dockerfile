pipeline {
  agent any
  stages {
    stage('begin') {
      steps {
        echo 'hello world'
      }
    }
    stage('checkout') {
      steps {
        echo 'checkout'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins-pipe-github', url: 'https://github.com/bcyup/dockerfile.git']]])
      }
    }
    stage('Build') {
            steps {
                echo '开始编译构建'
                sh '''docker build -t bcyup/agones:pipe111 -f 	php-fpm_dockerfile	.'''
            }
    }
    stage('Push') {
            steps {
                echo '推送'
                echo 'login in dockerhub'
                sh '''docker login -u bcyup -p yup1030WUYANYING 
                      docker push bcyup/agones:pipe111'''
            }
     }
     stage('clean') {
            steps {
                echo '清理'
                sh 'docker rmi bcyup/agones:pipe111'
            }
        } 
    
  }
  post {
    success {
      echo 'ok！！！'
    }
  }
  environment {
    name = 'jenkins-pipe'
  }
}
