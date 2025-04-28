pipeline {
  agent {
    node {
      label 'Slave-01'
    }

  }
  stages {
    stage('Build') {
      steps {
        bat 'mvn -B -DskipTests clean package'
      }
    }

    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }

      }
      steps {
        bat 'mvn test'
      }
    }

    stage('Sonar-Report') {
      steps {
        bat 'mvn clean install sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqa_facbbb3ab1b3fb66a29e8def13266576f4ffbc2e'
      }
    }
    stage('Deploy') {
    steps {
        bat 'start java -jar target/java-webapp-1.0.jar'
      }
    }
  }
}
