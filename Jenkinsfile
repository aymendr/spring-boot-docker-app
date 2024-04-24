pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              bat "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
      }
      stage('Unit Tests') {
            steps {
              bat "mvn test"
            }
      }


  }
}