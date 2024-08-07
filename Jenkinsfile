pipeline {
    agent any
        environment {
        mvnHome = tool 'maven'
        tomcatUser = 'ec2-user'
        tomcatHost = '13.201.168.125'
        tomcatPath = '/opt/tomcat/webapps/'
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
                archiveArtifacts artifacts: '*/target/.war'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy the artifact using rsync and ssh
                sshagent(['ssh']) {
                    sh "rsync -avz -e 'ssh -o StrictHostKeyChecking=no' --delete target/*.war ${tomcatUser}@${tomcatHost}:${tomcatPath}"
                }
            }
        }
    }
}
