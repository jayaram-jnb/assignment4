pipeline {
        agent any
        node {
def mvnHome
def tomcatUser = 'ec2-user'
def tomcatHost = '13.233.56.73'
def tomcatPath = '/opt/tomcat/apache-tomcat-9.0.68/webapps/'
stage('Checkout') {
// Checkout source code from Git
git branch: 'master', credentialsId: 'gittoken', url:
'https://github.com/jayaram-jnb/java-example-maven.git'
}
stage('Build') {
// Set Maven tool
mvnHome = tool 'Maven'
// Run Maven build
sh "'${mvnHome}/bin/mvn' clean package"
// Archive the build artifacts
archiveArtifacts artifacts: '**/target/*.war'
}
stage('Deploy') {
// Deploy the artifact using rsync and ssh

sshagent(['ssh']) {
sh "rsync -avz -e 'ssh -o StrictHostKeyChecking=no' --delete target/*.war
${tomcatUser}@${tomcatHost}:${tomcatPath}"
}
}
}
}
