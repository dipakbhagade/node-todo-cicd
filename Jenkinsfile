pipeline {
   agent {label 'PR-agent'}
     stages{
	   stage('code'){
	     steps{
		   git url:'https://github.com/dipakbhagade/node-todo-cicd.git', branch:'master'
		   }
        }
		stage('Build and test'){
	     steps{
		   sh 'docker build . -t dipak1994/node-todo-cicd-app:latest'
		   }
        }		
		stage('login push image on dockerHub'){
	     steps{
		   echo 'login push image on dockerHub'
		     withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
		       sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
		       sh 'docker push dipak1994/node-todo-cicd-app:latest' 
		     }		   
		   }
        }		
		stage('Deploy'){
	     steps{
		   sh 'docker-compose down && docker-compose up -d'
		   }
        }		
	}
}
