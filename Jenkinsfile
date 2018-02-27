pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''JAVA_HOME=/opt/java/jdk-9.0.4
export JAVA_HOME

M2_HOME=/home/moazzams/maven
export M2_HOME
M2=$M2_HOME/bin
export M2

PATH=$PATH:$JAVA_HOME/bin
PATH=$PATH:$M2
export PATH
echo $PATH
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
        sh '''JAVA_HOME=/opt/java/jdk1.8.0_161
export JAVA_HOME

M2_HOME=/home/moazzams/maven
export M2_HOME
M2=$M2_HOME/bin
export M2

PATH=$PATH:$JAVA_HOME/bin
PATH=$PATH:$M2
export PATH
echo $PATH
mvn test'''
      }
    }
    stage('Deploy') {
      steps {
        sh '''scp -i \'/home/moazzams/Downloads/jenkintomcat(1).pem\' \'./target/blog-0.0.1-SNAPSHOT.war\' ec2-user@ec2-34-253-164-120.eu-west-1.compute.amazonaws.com:/tmp/
'''
      }
    }
  }
}