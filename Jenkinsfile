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
				echo "Code deployed."
			}
		}
	}
}
