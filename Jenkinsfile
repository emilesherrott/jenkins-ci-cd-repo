pipeline {
    agent any
    // # NEW CONFIG
    environment {
        dockerHome = tool "myDocker"
        mavenHome = tool "myMaven"
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'docker --version'
                // sh 'mvn --version'
                // sh 'node --version'
                echo 'Build'
                // Whats the path
                echo "Path: $PATH"
                // What"s the build number
                echo "Build Number: $env.BUILD_NUMBER"
                // Whats the build id
                echo "Build ID: $env.BUILD_ID"
                // What"s the build tag
                echo "Build Tag: $env.BUILD_TAG"
                // What"s the build url
                echo "Build URL: $env.BUILD_URL"
                // What"s the job name
                echo "Job Name: $env.JOB_NAME"
            }
        }
	}
}