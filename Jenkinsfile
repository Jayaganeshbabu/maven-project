def abc="test"

pipeline {
  agent any
  options{
    timestamps()
  }
  stages {
    stage("Checkout") {
      steps {
        script {
          dir("code") {
            sh "echo This is checkout stage"
            checkout scm
          }
        }
      }
    }
    stage("Build") {
      steps {
        script {
          dir("code") {
            withMaven(maven: 'mvn') {
              sh "mvn clean install"
            }
          }
        }
      }
    }
    stage('SonarQube Analysis') {
      steps {
        withMaven(maven: 'mvn') {
          withSonarQubeEnv('My Sonar Server') {
            sh "mvn clean verify sonar:sonar -Dsonar.projectKey=DevOpsTest"
          }
        }
      }
    }
  }
}
