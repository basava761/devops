node{

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '2', numToKeepStr: '1')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])


echo "jobname is:${env.JOB_NAME}"
echo "build id is is:${env.BUILD_ID}"
echo "build number is is:${env.BUILD_NUMBER}"

def mavenHome= tool name:'maven3.8.7'

stage('Checkout'){
git credentialsId: 'c515a88b-3030-47c7-af75-cd6de491007f', url: 'https://github.com/basava761/maven-web-application.git'
}
stage('Building'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('Executing sonarreport'){
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('Executing sonarreport'){
sh "${mavenHome}/bin/mvn clean deploy"
}
stage('Deploy to tomcat'){
sshagent(['7c3aa961-e885-44ef-9bef-71d8b6a312ed']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.164.227:/opt/tomcat/webapps/"

}
}




}
