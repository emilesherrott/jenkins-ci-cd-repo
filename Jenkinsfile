pipeline {
    agent any
    environment {
        dockerHome = tool "myDocker"
        mavenHome = tool "myMaven"
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'mvn --version'
                sh 'docker --version'
                echo 'Checkout'
                echo "Path: $PATH"
                echo "Build Number: $env.BUILD_NUMBER"
                echo "Build ID: $env.BUILD_ID"
                echo "Build Tag: $env.BUILD_TAG"
                echo "Build URL: $env.BUILD_URL"
                echo "Job Name: $env.JOB_NAME"
            }
        }
		stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
		stage('Test') {
    		steps {
        		sh "mvn test"
    		}
		}
		stage('Package') {
    		steps {
       			sh "mvn package -DskipTests"
    		}
		}
		stage('Build Docker Image'){
    		steps {
				script {
            		dockerImage = docker.build("emilesherrott/currency-exchange-devops:${env.BUILD_TAG}")
       			}
        
   			}
		}
		stage('Push Docker Image'){
    		steps {
        		script {
					docker.withRegistry('', 'dockerhub') {
            			dockerImage.push()
            			dockerImage.push('latest')
					}
        		}
    		}
		}
	}
}