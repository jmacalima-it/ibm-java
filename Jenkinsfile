node{

  def dockerRun = 'docker run -d -p 80:8080 --name auto-java jmacalimait/java-test:helloworld'
 
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
sh 'docker tag java-helloworld jmacalimait/java-test:helloworld'

}

  stage ('Push Docker image to DockerHub') {



sh 'docker push jmacalimait/java-test:helloworld'

}
  
  stage ('Deploy to Dev') {
    
 
    
sshagent(['dserver']) {

  sh "ssh -o StrictHostKeyChecking=no ubuntu@52.53.43.187 ${dockerRun}"

}


  }
    
}
