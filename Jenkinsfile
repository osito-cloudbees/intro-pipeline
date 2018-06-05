pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('say hello') {
      steps {
        echo "Hello ${params.Name}!"
        sh 'java -version'
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
      }
    }
    stage('Testing') {
        failFast true
        parallel {
          stage('Java 8') {
            agent { label 'jdk8' }
            steps {
              sh 'java -version'
              sleep time: 10, unit: 'SECONDS'
            }
          }
          stage('Java 9') {
            agent { label 'jdk9' }
            steps {
              sh 'java -version'
              sleep time: 20, unit: 'SECONDS'
            }
          }
        }
      }
        stage('Checkpoint') {
         agent none
         steps {
            checkpoint 'Checkpoint'
         }
      }
    stage('Deploy'){
      echo 'Deploying...'
    }
  }
  environment {
    MY_NAME = 'David'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
    post {
    aborted {
      echo 'Why didn\'t you push my button?'
    }
  }

}
