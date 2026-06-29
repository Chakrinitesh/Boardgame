pipeline {
  agent any

  tools {
    maven 'maven'
  }

  environment {
    SCANNER_HOME = tool 'sonar-scanner'
  }
  stages {
    stage('Git Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Chakrinitesh/Boardgame.git'
      }
    }

    stage('Compile') {
      steps {
        sh "mvn compile"
      }
    }

    stage('Test') {
      steps {
        sh "mvn test"
      }
    }
    stage('Package') {
      steps {
        sh "mvn package"
       }
    }
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonarqube') {

          sh '''
              $SCANNER_HOME/bin/sonar-scanner \
            -Dsonar.projectName=bloggingApp \
            -Dsonar.projectKey=bloggingApp \
            -Dsonar.java.binaries=target '''
          
           sh "echo $SCANNER_HOME"

        }
      }
    }
  }
}