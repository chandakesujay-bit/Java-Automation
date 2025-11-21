pipeline {

  agent any

  stages {

    stage('Checkout') {
      steps {
        git 'https://github.com/chandakesujay-bit/Java-Automation.git'
      }
    }

    stage('Build WAR') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'tomcat-credentials',
          usernameVariable: 'USER',
          passwordVariable: 'PASS'
        )]) {

          sh '''
          curl -u $USER:$PASS \
            --upload-file target/*.war \
            "http://3.6.86.102:8080/manager/text/deploy?path=/JavaAutomation&update=true"
          '''
        }
      }
    }
  }
}
