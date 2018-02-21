pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''export MAVEN_HOME=/maven
export PATH=$PATH:$MAVEN_HOME/bin
mvn clean install -Pprod -DskipTests'''
      }
    }
    stage('Test') {
      steps {
        sh '''export M2_HOME=/opt/apache-maven-3.5.2
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
mvn test'''
      }
    }
    stage('Deploy') {
      steps {
        cleanWs(cleanWhenSuccess: true)
      }
    }
  }
}