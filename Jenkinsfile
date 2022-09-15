pipeline {
  environment {
    registry = "http://3.110.86.199:8083/repository/docker-group/"
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
          sh 'sudo docker build -t flask-app:2.0 -f ./Dockerfile.txt .' 

        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	  sh 'sudo docker tag flask-app 3.110.86.199:8083/repository/docker-group/flask-app:2.0'
	  sh 'sudo docker login -u admin -p pooja 3.110.86.199:8083/repository/docker-group/' 
          sh 'sudo docker push 3.110.86.199:8083/repository/docker-group/flask-app:2.0'
          sh 'sudo docker logout 3.110.86.199:8083/repository/docker-group/'
          // sh 'curl -XGET "admin:pooja" -X PUT http://3.110.86.199:8081/repository/python/flask-app '
	    }
          }
        }
      }
    }
 stage('scan and build Jar file') {
      steps{
	  script {
	       withSonarQubeEnv()
        //   sh 'mvn clean package sonar:sonar' 
	     //sh "${scannerHome}/bin/sonar-scanner"
		sh './gradlew sonarqube'


	      }
            }
          }

        
