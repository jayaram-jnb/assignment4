pipeline {
        agent any
        stages {
        stage('Checkout') {
                          steps {
                          git branch: 'main', url: 'https://github.com/jayaram-jnb/java-example-maven.git'
                              }
                        }
        stage('Test') {
                        steps {
                        sh 'mvn test'
                            }
                    }
        stage('Build') {
                      steps {
                      sh 'mvn package'
                          }
                    }
      stage('Deploy') {
                      steps {
                      sh 'scp target/works-with-heroku-1.0.war ec2-user@18.60.101.31:/opt/tomcat/webapps/'
                            }
                    }
            }
      }
