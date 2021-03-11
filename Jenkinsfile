// scripted pipeline approach
// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Test"
// 	}
// }

// Declarative pipeline approach

pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3' } }

	environment{
		mavenHome = tool 'my-maven'
		dockerHome = tool 'my-docker'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps {
				sh 'docker --version'
				sh 'mvn --version'
			}
		}

		stage('Build'){
			steps {
				// download all depndencies
				sh "mvn clean compile"
			}
		}

		stage('Test'){
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				// create jar files and skip tests
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				// docker build -t  saadabdull4h/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("saadabdull4h/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image') {
			steps {
				script{
					// repo (empty: default), credential id
					dcoker.withRegistry('', 'dockerhub'){
						dockerImage.push();
						// ('<tag>')
						dockerImage.push('latest');
					}
					
				}
			}
		}

	}
	post {
		always {
			echo "run always"
		}
		success {
			echo "run when successful"
		}
		failure {
			echo "run when fail"
		}
		//changed when status of a build changes from, ex:failed to success
	}
}