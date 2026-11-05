pipeline {
  agent any
  environment {
    IMAGE = "jenkins-ci-demo"
  }
  stages {
    stage('Clone') {
      steps {
        checkout scm
        sh 'ls -la'
      }
    }
    stage('Build Docker image') {
      steps {
        sh 'docker build -t $IMAGE:$BUILD_NUMBER .'
      }
    }
    stage('Verify image') {
      steps {
        sh 'docker run --rm $IMAGE:$BUILD_NUMBER python -c "import flask; print(flask.__version__)"'
      }
    }
  }
  post {
    success {
      echo "Build #${env.BUILD_NUMBER} succeeded"
    }
    failure {
      echo "Build #${env.BUILD_NUMBER} FAILED"
      // notification step is added once Slack or email is configured
    }
  }
}
