pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh 'mvn clean install -Pprod -DskipTests'
          }
        }
        stage('Var') {
          steps {
            sh '''export PATH =$PATH:/usr/lib/jvm/java-8-openjdk-amd64/bin:/maven/bin:maven/bin
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