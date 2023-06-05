

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
    }
environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}
     stage('Login') {

			steps {
				bat 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				bat 'docker push dockerpush/nodeapp:latest'
			}
		}
	}

	post {
		always {
			bat 'docker logout'
		}
   
	}

