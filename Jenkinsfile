pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/jayaram-jnb/HelloWorld.git'
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['ssh']) {
                    sh '''
                        rsync -e "ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no" \
                        -avz --progress --rsync-path=/usr/bin/rsync target/works-with-heroku-1.0.war \
                        ec2-user@13.233.137.133:/opt/tomcat/webapps/
                    '''
                }
            }
        }
    }
}
