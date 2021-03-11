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
		mavenrHome = tool 'my-maven'
		dockerHome = tool 'my-docker'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build'){
			steps {
				sh 'docker --version'
				sh 'mvn --version'
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
			}
		}
		stage('Test'){
			steps {
				echo 'Test'
			}
		}
		stage('Integration Test'){
			steps {
				echo 'Integration Test'
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