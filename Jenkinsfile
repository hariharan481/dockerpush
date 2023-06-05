

pipeline{
    agent any
    

    stages {
        stage('Build') {
            steps {
      checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'dockerhub', url: 'https://github.com/hariharan481/dockerpush.git']])
                bat 'npm install'
            }
        }
         stage('Build Docker image') {
     steps {
        script {
          docker.build("17-alpine").run('-p 8009:3000')
        }
      }


    }
     stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubpwd')]) {
                   bat 'docker login -u hariharancute -p ${hari@2002}'

}
                   bat 'docker push javatechie/devops-integration'
                }
            }
        }
    
}
}
    




    

     

