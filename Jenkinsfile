node{

stage ('scm checkout') {

git 'https://github.com/jmacalima-it/ibm-java.git'
  sh “git checkout master”
}


stage (‘package stage’) {

sh label: ‘’, script: ‘mvn clean package ‘

}

}
