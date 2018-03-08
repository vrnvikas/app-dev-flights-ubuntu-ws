FROM jenkins:2.19.4-alpine

ENV JENKINS_REF /bitnami/jenkins





# copy scripts and ressource files
COPY jenkins-home/*.* $JENKINS_REF/
#COPY jenkins-home/userContent $JENKINS_REF/userContent
COPY jobs $JENKINS_REF/jobs/
COPY init.groovy.d $JENKINS_REF/init.groovy.d/
