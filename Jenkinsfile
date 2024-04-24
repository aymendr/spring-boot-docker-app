pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              bat "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
      }
      stage('Unit Tests and Jacoco reports') {
            steps {
              bat "mvn test"
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    jacoco execPattern: 'target/*.exec'
                }
            }
      }
      stage('Docker Build and Push') {
            steps {
              bat "printenv"
              bat "docker build -t aymendr/numeric-app:$GIT_COMMIT ."
              bat "docker push aymendr/numeric-app:$GIT_COMMIT"
            }
      }      
  }
}