pipeline{
	agent{label 'dev-test'}
  
	stages{
		stage('code') {
			steps{
				git url: 'https://github.com/dsparta/react_django_demo_app.git' , branch: 'main'			
			}				
		}
		stage('test and build') {
			steps{
				sh 'docker build . -t dsoum2023/react-todo:latest'
			}				
		}
		stage('docker login and push image') {
			steps{
				echo 'docker logging in and pushing image to docker-hub'
				withCredentials([usernamePassword(credentialsId:'DockerHub', passwordVariable: 'pass',usernameVariable: 'user')]){
				sh "docker login -u ${env.user} -p ${env.pass}"
				sh "docker push dsoum2023/react-todo:latest"
				}
			}				
		}
		stage('deploy') {
			steps{
				sh 'docker-compose down && docker-compose up -d'
			}				
		}
	}
}
