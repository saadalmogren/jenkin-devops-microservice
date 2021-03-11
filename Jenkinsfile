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
				sh "mvn failsafe:integeration-test failsafe:verify"
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