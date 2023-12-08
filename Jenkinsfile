pipeline {
    agent {
     label 'Jenkins-Agent' 
    }
  tools {
    jdk 'Java17'
    maven 'Maven3'
  }

  stages {
    stage ("Cleanup Workspace") {
      steps {
        cleanWs()
      }
    }

    stage ("Checkout from SCM") {
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/Gabinsime75/register-app_application-repo.git'
      }
    }

    stage ("Build Application") {
      steps {
        sh "mvn clean package"
      }
    }

    stage ("Test Application") {
      steps {
        sh "mvn test"
      }
    }

    stage ("SonarQube Analysis") {
      steps {
        script {
           withSonarQubeEnv(credentialsID: 'jenkins-sonarqube-token') {
               sh "mvn sonar:sonar"
           } 
        }
      }
    }

    stage ("Quality Gate"){
      steps {
        script {
           waitForQualityGate abortPipeline: false, credentialsID: 'jenkins-sonarqube-token'
        }
      }
    }
  }
}
