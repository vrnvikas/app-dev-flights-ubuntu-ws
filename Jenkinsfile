
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
                 sh 'mvn clean package'
            }

        }
    }
    
}


	


	


	
	
	 
