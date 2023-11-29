pipeline {
    agent {
        docker {
            image 'maven:3.6.1-alpine'
            args '-v /root/.m2:/root/.m2'
            }
        }
    parameters {
        string(name: 'branch', defaultValue: 'master', description: 'Git branch')
    }
    stages{
        stage('同步源码') {
            steps {
                git url:'git@github.com:Gh-chenqiang/simple-java-maven-app.git', branch:"$params.branch"
            }
        }

        stages {
            stage ('Build') {
                steps {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
            stage('Test') {
                steps {
                    sh 'mvn test'
                }
                post {
                    always {
                        junit 'target/surefile-report/*.xml'
                    }
                }
            }
        }
    }
}