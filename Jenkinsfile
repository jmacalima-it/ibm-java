node{

stage ('scm checkout') {

git branch: 'main', url: 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm
}


stage ('package stage') {

sh label: '', script: 'mvn clean package '

}

}
