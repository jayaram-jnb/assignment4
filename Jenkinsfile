pipeline {
        agent any
        tools {
                maven "maven"
            }
        stages {
        stage('Checkout') {
                          steps {
                          git branch: 'main', url: 'https://github.com/jayaram-jnb/HelloWorld.git'
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
                      sh 'scp target/works-with-heroku-1.0.war ec2-user@13.233.56.73:/opt/tomcat/webapps/'
                            }
                    }
            }
      }
