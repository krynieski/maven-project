pipeline {
	agent any
	stages {

		stage ('Build') {
			steps {
				echo "Building..."
				sh '/media/krynieski/Media/Dokumenty/Nauka/2018/CI_Training/tools/apache-maven-3.6.0/bin/mvn clean package'
			}
			post {
				success {
					echo "Now Archiving..."
					archiveArtifacts artifacts: '**/target/*.war'
					echo "Artifacts archived."
				}
			}
		}

		stage ('Deploy to Staging') {
			steps {
				echo "Deploying to staging env..."
				build job: 'PipelineAsCode-deploy-to-staging'
				echo "Code deployed."
			}
		}

		stage ('Deploy to Production') {
			steps {
				timeout(time:5, unit:'DAYS') {
					input message:'Approve PRODUCTION Deployment?'
				}

				build job: 'PipelineAsCode-deploy-to-prod'
			}

			post {
				success {
					echo "Code depoyed to Production"
				}

				failure {
					echo "Deployment failed!"
				}
			}
		}
	}
}
