pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/MoonSung88/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t goldoh88/test:newnewmain .
        sudo docker push goldoh88/test:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl create deploy testpipeline --image=goldoh88/test:newnewmain
        sudo kubectl expose deploy testpipeline --type=NodePort --port=8081 \
        --target-port=80 --name=testpipeline-svc
        '''
      }
    }
  }
}
