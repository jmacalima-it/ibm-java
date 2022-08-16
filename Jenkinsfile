node{

stage ('scm checkout') {
  steps {
git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm
  }
}


stage ('package stage') {
  steps {
sh 'chmod +x mvnw'
sh label: '', script: 'mvnw clean package '

  }
}

}
