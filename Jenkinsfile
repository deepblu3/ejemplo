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
                sh 'docker rm $(docker ps -a -q)'
                sh 'docker run --name app -d -p 80:80 app:test'
                sh '/bin/nc -vz localhost 80'
                sh 'docker stop app'
		    }
		}
		stage('Deploy - Push registry') {
		steps {
		    echo 'DEPLOY'
		    withCredentials([usernamePassword(credentialsId: '9d97489d-bf4c-4be5-9e1d-d2a910ee94ef', passwordVariable: 'pass_docker', usernameVariable: 'user_docker')]) {
            	sh 'docker tag app:test solidge0/app:stable'
            	sh 'docker push  solidge0/app:stable'
            }

			}
		}
	}
}	