pipeline {
  environment {
    registry = "http://3.110.86.199:8081/repository/docker-group/"
    registryCredential = 'nexusrepo'
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/pmoghle/task2.git'
      }
    }
   stage('Building image') {
      steps{
        script {
          sh 'sudo docker build -t flask-app -f ./Dockerfile.txt .' 

        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
           sh 'curl -XGET "admin:pooja" -X PUT http://3.110.86.199:8081/repository/docker-group/flask-app -T flask-app'
	    }
          }
        }
      }
    }

        
