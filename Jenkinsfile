node{

stage ('scm checkout') {

git 'https://github.com/jmacalima-it/ibm-java.git'
  checkout scm
}


stage ('package stage') {

sh label: '', script: 'mvn clean package '

}

}
