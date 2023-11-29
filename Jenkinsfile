pipeline {
    agent {
        docker {
            image '3.8.6-jdk-11'
            args '-v /Users/chenqiang/.m2:/root/.m2'
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