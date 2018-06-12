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
                sh 'docker run --name app -d -p 80:80 app:test'
                sh '/bin/nc -vz localhost 80'
                sh 'docker stop app'
		    }
		}
		stage('Deploy - Push registry') {
		steps {
		    echo 'DEPLOY'
		    withCredentials([usernamePassword(credentialsId: 'solidge0_docker', passwordVariable: 'pass', usernameVariable: 'user')]) {
            	sh 'docker tag app:test solidge0/app:stable'
            	sh 'docker push  solidge0/app:stable'
            }

			}
		}
	}
}	