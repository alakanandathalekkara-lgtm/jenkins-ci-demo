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
      mail to: 'alakanandathalekkara@gmail.com',
           subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Build #${env.BUILD_NUMBER} of ${env.JOB_NAME} failed.\nDetails: ${env.BUILD_URL}console"
    }
  }
}
