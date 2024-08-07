pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/jayaram-jnb/java-example-maven.git'
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['ssh']) {
                    sh '''
                        sudo rsync -e "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no" \
                        -avz --progress --rsync-path=/usr/bin/rsync target/works-with-heroku-1.0.war \
                        ec2-user@13.201.168.125:/opt/tomcat/webapps/
                    '''
                }
            }
        }
    }
}
