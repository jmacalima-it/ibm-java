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

sh 'docker build -t java-helloworld .'
sh 'docker tag java-helloworld jmacalimait/java-test:java-helloworld'

}

  stage ('Push Docker image to DockerHub') {

withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pdocker', usernameVariable: 'udocker')]) {

sh 'docker login -u ${udocker} -p ${pdocker}'

}

sh 'docker push jmacalimait/java-test:java-helloworld'

}
  
}
