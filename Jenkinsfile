node{

  def dockerRun = 'docker run -d -p 80:8080 --name auto-java jmacalimait/java-test:java-helloworld'
  def dockerLogin = 'docker login -u ${udocker} -p ${pdocker}'
stage ('scm checkout') {

git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm

}


stage ('package stage') {

sh 'chmod +x mvnw'
sh label: '', script: './mvnw clean package '


}
  
  stage ('docker image build') {

sh 'docker build -t java-helloworld .'
sh 'docker tag java-helloworld jmacalimait/java-test:java-helloworld'

}

  stage ('Push Docker image to DockerHub') {

withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pdocker', usernameVariable: 'udocker')]) {

sh 'docker login -u ${udocker} -p ${pdocker}'

}

sh 'docker push jmacalimait/java-test:java-helloworld'

}
  
  stage ('Deploy to Dev') {
    
    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pdocker', usernameVariable: 'udocker')]) 

    
sshagent(['dserver']) {

  sh "ssh -o StrictHostKeyChecking=no ubuntu@52.53.43.187 ${dockerLogin} && ${dockerRun}"

}

}
  
}
