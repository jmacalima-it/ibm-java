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

withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'p-docker', usernameVariable: 'u-docker')]) {

sh "docker login -u ${u-docker} -p ${p-docker}"

}

sh 'docker push jmacalima/java-helloworld'

}
  
}
