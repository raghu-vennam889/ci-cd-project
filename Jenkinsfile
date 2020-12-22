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
			sh 'docker tag sa-frontend raghuram889/sa-frontend'
			sh 'docker tag sa-webapp raghuram889/sa-webapp'
			sh 'docker tag sa-logic raghuram889/sa-logic'
			sh 'docker push raghuram889/sa-frontend'
			sh 'docker push raghuram889/sa-webapp'
			sh 'docker push raghuram889/sa-logic'
		}
	}
	stage('deploy to kubernetes') {  
		steps {
			sh 'cd ${workspace}/resource-manifests && kubectl apply -f .'
		}
	}
	
   }
}
