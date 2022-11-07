pipeline {
  agent {
    label "jenkins-node"
  }

  triggers {
    //pollSCM('* * * * *')
    githubPush()
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/dbfan24/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://54.180.24.249:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}
