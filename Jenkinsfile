pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''export PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin:/$MAVEN_HOME/bin
mvn clean install -Pprod -DskipTests'''
          }
        }
        stage('Var') {
          steps {
            sh '''export PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin
echo $PATH'''
          }
        }
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