pipeline {
agent any

	stages {
		stage('build sa-frontend') {
		steps {
			sh 'cd ${WORKSPACE}/sa-frontend && npm install && npm run build'
		}
	}
	stage('Build sa-webapp') {
		steps {
			sh 'cd ${WORKSPACE}/sa-webapp && mvn install'
		}
	}
	stage ('build docker sa-frontend') {
		steps {
			sh 'cd ${WORKSPACE}/sa-frontend && docker build -t sa-frontend .'
		}
	}
	stage ('build docker sa-webapp') {
		steps {
			sh 'cd ${WORKSPACE}/sa-webapp && docker build -t sa-webapp .'
		}
	}
	stage ('buold docker sa-logic') {
		steps {
			sh 'cd ${WORKSPACE}/sa-logic && docker build -t sa-logic .'
		}
	}	
		
	stage('push to registry') {
		steps {
			withDockerRegistry{[ credentialsId: "harbor", url:"https://harbor.devopsdoor.com/"]} {
			sh 'docker tag sa-frontend 54.205.127.4/cicd-prod/sa-frontend'
			sh 'docker tag sa-webapp 54.205.127.4/cicd-prod/sa-webapp'
			sh 'docker tag sa-logic 54.205.127.4/cicd-prod/sa-logic'
			sh 'docker push 54.205.127.4/cicd-prod/sa-frontend'
			sh 'docker push 54.205.127.4/cicd-prod/sa-webapp'
			sh 'docker push 54.205.127.4/cicd-prod/sa-logic'
			}	
		}
	}
	stage('deploy to kubernetes') {  
		steps {
			sh 'cd ${WORKSPACE}/resource-manifests && kubectl apply -f .'
		}
	}
	
	
   }
}
