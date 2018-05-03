pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello ${params.Name}!') {
      steps {
        echo 'Hello ${params.Name}!'
        sh 'java -version'
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
      }
    }
    stage('Deploy') {
      options {
        timeout(time: 30, unit: 'SECONDS')
      }
      input {
        message 'Which Version?'
        id 'Deploy'
        parameters {
          choice(name: 'APP_VERSION', choices: '''v1.1
v1.2
v1.3''', description: 'What to deploy?')
        }
      }
      steps {
        echo "Deploying ${APP_VERSION}."
      }
    }
    stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
        
      }
    }
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }
  }
  environment {
    MY_NAME = 'Ed'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'Who should I say hi to?')
  }
}