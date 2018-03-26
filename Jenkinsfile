
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

        // stage('munit') {

        //     steps {
                 

        //        sh 'mvn -U clean test cobertura:cobertura -Dcobertura.report.format=xml'
        //         junit '**/target/*-reports/TEST-*.xml'
        //         step([$class: 'CoberturaPublisher', coberturaReportFile: 'target/site/cobertura/coverage.xml'])


        //     }


        // }

        // stage('Sonar') {
        //     steps {
        //         sh "mvn sonar:sonar -Dsonar.host.url=${env.SONARQUBE_HOST}"
        //     }
        // }

        // stage('publish munit result') {
        //     steps {

        //         publish_html()
        //     }
        // }

        // stage('push to artifactory') {
        //     steps {

        //         configFileProvider([configFile(fileId: 'our_settings', variable: 'SETTINGS')]) {
        //             sh "mvn -s $SETTINGS deploy -DskipTests -Dartifactory_url=${env.ARTIFACTORY_URL} -Dartifactory_name=${env.ARTIFACTORY_NAME}"
        //         }
        //     }
        // }


        stage('tag the build') {
            steps { 


                    
                    sh"git config user.name 'vrnvikas'"
                    sh"git config user.email 'vrnvikas1994@gmail.com'"
                    //sh"git tag v$pom_version.${env.BUILD_NUMBER}"
                    //sh"git push -u ${repo_artifactory_path} master tag v$pom_version.${env.BUILD_NUMBER}"
                    sh 'git describe --tags --long'
                    sh "git tag -a v0.8.1 -m 'build-${env.BUILD_NUMBER}'"
                    sh 'git push origin v0.8.1'
                    print "commit message"
                    print getCommit()
                    print "tag"
                    print sh(script: "git describe --tags --long", returnStdout: true)?.trim()
            }
        }
               
        
    }
    
}

/** @return The tag name, or `null` if the current commit isn't a tag. */
String gitTagName() {
    commit = getCommit()
    if (commit) {
        desc = sh(script: "git describe --tags ${commit}", returnStdout: true)?.trim()
        if (isTag(desc)) {
            return desc
        }
    }
    return null
}
 
/** @return The tag message, or `null` if the current commit isn't a tag. */
String gitTagMessage() {
    name = gitTagName()
    msg = sh(script: "git tag -n10000 -l ${name}", returnStdout: true)?.trim()
    if (msg) {
        return msg.substring(name.size()+1, msg.size())
    }
    return null
}
 
String getCommit() {
    return sh(script: 'git rev-parse HEAD', returnStdout: true)?.trim()
}
 
@NonCPS
boolean isTag(String desc) {
    match = desc =~ /.+-[0-9]+-g[0-9A-Fa-f]{6,}$/
    result = !match
    match = null // prevent serialisation
    return result
}

def publish_html()
{   
    def exists = fileExists 'target/munit-reports/coverage/summary.html'
    if (exists) 
    {
        echo 'html report file is generated'
        publishHTML (target: [
        allowMissing: false,
        alwaysLinkToLastBuild: false,
        keepAll: true,
        reportDir: 'target/munit-reports/coverage',
        reportFiles: 'summary.html',
        reportName: "Coverage Report" ])
    } 
        
}