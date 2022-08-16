node{

stage ('scm checkout') {

git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm

}


stage ('package stage') {

sh 'chmod +x mvnw'
sh label: '', script: './mvnw clean package '


}
  
  stage ('docker image build') {

sh 'docker build -t jeff/java-helloworld .'

}

  stage ('Push Docker image to DockerHub') {

withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {

sh "docker login -u jmacalimait -p ${dockerhubaccount}"

}

sh 'docker push jmacalima/java-helloworld'

}
  
}
