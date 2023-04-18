pipeline{
  agent{ label 'dev-test'}
  
    stages {
      stage('code'){
        steps{
          git url: 'https://github.com/dsparta/react_django_demo_app.git' , branch: 'main'
        }    
      }
      stage('build and test'){
        steps{
          sh 'docker build . -t dsoum2023/react-todo:latest'
        }    
      }
      stage('Docker login and push Image to docker-hub'){
        steps{
          echo "docker login and pushing Image...."
          withCredentials([usernamePassword(credentialsId: 'DockerHub',passwordVariable: 'pass' , usernameVarible: 'user')]){
            sh 'docker login -u ${env.user} -p ${env.pass}'
            sh 'docker push dsoum2023/react-todo:latest'
            }
        }
      }
      stage('deploy'){
       steps{
          sh 'docker-compose down && docker-compose up -d'
       }    
      }
            
    }
  
  }



}
