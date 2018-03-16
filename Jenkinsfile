
pipeline {
    agent any
    tools {
        jdk 'jdk8'
        maven 'maven3'
    }
    
    stages {
        stage('download_stash_code') {
            steps {
                checkout scm
            }
        }
        
        stage('clean') {
        
            steps {
                 sh 'mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml'
            }

            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                }
            }

        }

        stage('Sonar') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
            }
        }
    }
    
}


	


	


	
	
	 
