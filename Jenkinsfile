

pipeline{
    agent any
    
environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
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
    stage('Login') {
			steps {
				bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u hariharancute --password-hari@2002'
			}
		}

		stage('Push') {

			steps {
				bat 'docker push hariharan481/dockerpush:latest'
			}


            post {
		always {
			bat 'docker logout'
		}
   
	}
		}
	

	
    }
}
    




    

     

