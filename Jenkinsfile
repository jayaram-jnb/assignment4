pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/jayaram-jnb/java-example-maven.git'
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    def artifact = 'target/works-with-heroku-1.0.war'
                    def remoteHost = 'ec2-user@13.233.56.73'
                    def remotePath = '/opt/tomcat/webapps/'
                    
                    sh "rsync -avz ${artifact} ${remoteHost}:${remotePath}"
                    // Optional: Restart Tomcat
                    sh "ssh ${remoteHost} 'sudo systemctl restart tomcat'"
                }
            }
        }
    }
}
