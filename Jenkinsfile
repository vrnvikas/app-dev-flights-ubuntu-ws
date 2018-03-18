
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
                sh 'mvn clean'
            }
        }

        stage('munit') {

            steps {
                 sh 'mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml'
                junit '**/target/munit-reports/coverage/*.xml'
                step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])
            }


        }

        // stage('Sonar') {
        //     steps {
        //         sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
        //     }
        // }

        // stage('push to artifactory') {
        //     steps {

        //         configFileProvider([configFile(fileId: 'our_settings', variable: 'SETTINGS')]) {
        //             sh "mvn -s $SETTINGS deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL}"
        //         }
        //     }
        // }        
        

    }
    
}