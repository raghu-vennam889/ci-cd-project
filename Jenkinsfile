pipeline {
<<<<<<< HEAD
<<<<<<< HEAD
    agent any
=======
agent {
    node {
        label 'master'
    }
}
>>>>>>> 52ef136ebb258c324a60cb90181ac223cc6bb02f

    stages {
        stage('Build sa-frontend') {
            steps {
                sh 'cd ${WORKSPACE}/sa-frontend && npm install && npm run build'
            }
        }
        stage('Build sa-webapp') {
            steps {
                sh 'cd ${WORKSPACE}/sa-webapp && mvn install'
            }
        }
        stage('Build Docker sa-frontend') {
            steps {
                sh 'cd ${WORKSPACE}/sa-frontend && docker build -t sa-frontend .'
            }
        }
        stage('Build Docker sa-webapp') {
            steps {
                sh 'cd ${WORKSPACE}/sa-webapp && docker build -t sa-webapp .'
            }
        }
        stage('Build Docker sa-logic') {
            steps {
                sh 'cd ${WORKSPACE}/sa-logic && docker build -t sa-logic .'
            }
        }
        stage('Push to registry') {
            steps {
                sh 'docker tag sa-frontend basilvarghese/sa-frontend'
                sh 'docker tag sa-webapp basilvarghese/sa-webapp'        
                sh 'docker tag sa-logic basilvarghese/sa-logic'        
                sh 'docker push basilvarghese/sa-frontend'
                sh 'docker push basilvarghese/sa-webapp'
                sh 'docker push basilvarghese/sa-logic'
            }
        }
        stage('Deploy to kubernetes') {
            steps {
                sh 'cd ${WORKSPACE}/resource-manifests && kubectl apply -f .'
            }
        }
        stage('Archieve Artifacts') {
            steps {
                archiveArtifacts '**/*.jar'
            }
        }
        stage('Email Notification') {
            steps {
                emailext body: 'Please check', subject: 'Build Failed', to: 'basil1987@gmail.com'
            }
        }

    }
=======
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
	stage('Archive Artifacts') {
		steps {
			archiveArtifacts '**/*.jar'
		}
	}
	stage('Email Notification') {
		steps {
			emailtext body: 'please check', subject: 'Build failed', to: 'raghu.vennam889@gmail.com'
		}
	}
   }
>>>>>>> dependabot/npm_and_yarn/sa-frontend/handlebars-4.7.6
}


