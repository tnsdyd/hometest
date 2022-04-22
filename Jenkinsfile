pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/tnsdyd/hometest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        echo "test" >> index.html
        sudo docker build -t mm0820/hometest:newmain . 
        sudo docker push mm0820/hometest:newmain
        
        echo "test12322" >> index.html
        sudo docker build -t mm0820/hometest:newblog . 
        sudo docker push mm0820/hometest:newblog
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kubectl set image deploy deploy-main ctn-main=mm0820/hometest:newmain
        sudo kubectl set image deploy deploy-main ctn-main=mm0820/hometest:newmain
	'''
      }
    }
  }
}

