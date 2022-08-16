pipeline {

  agent any
  
  environment {
  def dockerRun = 'docker run -d -p 80:8080 --name jenkins-java jmacalimait/java-test:helloworld'
    def test = 'test'
  }
    
  stages {
    
stage ('SCM checkout') {

  steps {
git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm
  }
  
}


stage ('Package Stage') {

  steps {
sh 'chmod +x mvnw'
sh label: '', script: './mvnw clean package '

  }
    
}
  
  stage ('Docker Image Build') {

    steps {
sh 'docker build -t java-helloworld .'
sh 'docker tag java-helloworld jmacalimait/java-test:helloworld'

    }
}

  stage ('Push Docker image to DockerHub') {

    steps {

sh 'docker push jmacalimait/java-test:helloworld'
    }
}
  
  stage ('Deploy to Dev') {
    
    steps {
    
sshagent(['dserver']) {

  sh "ssh -o StrictHostKeyChecking=no ubuntu@52.53.43.187 ${dockerRun}"

}
 }
  }
    
    
    
}
 //end stages
}  
 //end of pipelines
