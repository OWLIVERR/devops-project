pipeline {
    agent any
    tools {
        jdk 'jdk11'
        maven 'maven3' 
    }
    environment{
        SCANNER_HOME = tool 'sonarScanner'
    }
    stages{
        stage('Checkout git') {
             steps {
	            git branch: 'main', url: 'https://github.com/OWLIVERR/devops-project'
                }
            }
        stage ('Code Compile') {
	        steps {
		        sh 'mvn clean compile' 
	           }
            }
        node{
            stage('SCM') {
                checkout scm
            }
            stage('SonarQube Analysis') {
                def mvn = tool 'maven3';
                withSonarQubeEnv() {
                        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=ditiss-project"
                    }
            }
        }
       
    }
}
