pipeline {

  environment {
    dockerimagename = "rajarnd/react-app"
    dockerImage = ""
    DOCKERHUB_CREDENTIALS=credentials('dockerhub-credentials')
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/Lrnd-Devops1/jenkins-kubernetes-deployment.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
        //sh 'docker build -t bravinwasike/react-app .'
      }
    }
    stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push rajarnd/react-app:latest'
			}
		}
   

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}