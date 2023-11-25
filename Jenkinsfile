pipeline {
    agent {
     label 'Jenkins-Agent' 
    }
  tools {
    jdk 'java17'
    maven 'Maven3'
  }

  stages {
    stage ("Cleanup Eotkspace") {
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
  }
}
