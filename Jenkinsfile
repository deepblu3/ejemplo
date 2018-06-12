pipeline {
    agent any
	stages {
		stage('Build') {
		steps {
			sh 'docker build -t app:test .'
			}
		}
		stage('Test') {
		steps {
			echo 'TEST'
			sh 'docker run --rm --name app -p 80:80 app:test'
			sh '/bin/nc -vz localhost 8080'
			}
			post {
			    always {
			        sh 'docker container stop app'
			    }
			}
		}
		stage('Deploy - Push registry') {
		steps {
			echo 'DEPLOY'
			sh 'docker tag app:test solidge0/app:stable'
			sh 'docker push  solidge0/app:stable'
			}
		}
	}
}	