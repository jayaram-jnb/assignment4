pipeline {
    agent any
        environment {
        mvnHome = tool 'maven'
            }
    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from Git
                git branch: 'main', url: 'https://github.com/jayaram-jnb/java-example-maven.git'
            }
        }
        stage('Build') {
            steps {
                // Run Maven build
                sh "'${mvnHome}/bin/mvn' clean package"
                // Archive the build artifacts
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy the artifact using rsync and ssh
                sshagent(['ssh']) {
                   rsync -avz -e 'ssh -o StrictHostKeyChecking=no' --delete target/works-with-heroku-1.0.war ec2-user@13.201.168.125:/tmp/
            ssh -o StrictHostKeyChecking=no ec2-user@13.201.168.125 'sudo mv /tmp/works-with-heroku-1.0.war /opt/tomcat/webapps/'
                }
            }
        }
    }
}
