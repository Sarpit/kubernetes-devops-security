pipeline {
  agent any

  stages {
      stage('Build Artifact') {
        steps {
          sh "mvn clean package -DskipTests=true"
          archive 'target/*.jar' //so that they can be downloaded later
        }
      }

      stage('Test Code') {
        steps {
          sh 'mvn test'
        }
        post {
          always {
            junit 'target/surefire-reports/*.xml'
            jacoco (
              execPattern: 'target/jacoco.exec'
            )  
          }
        }
      }   
    }
}