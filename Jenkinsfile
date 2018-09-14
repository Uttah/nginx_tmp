pipeline {
  agent any
  stages {
    stage('Building image') {
      steps {
        echo "Building image"
        sh 'docker build -t nginx_test .'
      }
    }

    stage('Simple test') {
      steps {
        sh('''#!/bin/bash
          docker build -t nginx_test . && \\
          RESPONSE=`curl localhost:3000` || exit 1
          if [ \$RESPONSE != 'icoworld' ]; then
              exit 1
          fi
          ''')
      }
    }

    stage('Deploy') {
      steps {
        sh 'docker run -d -p 4444:80 nginx_test'
      }
    }
  }
}
