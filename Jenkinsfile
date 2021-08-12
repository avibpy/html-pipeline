pipeline {

    agent any
    
    environment {
        PASS = credentials('registry-pass') 
    }
#test
    stages {
s
        stage('Build') {
            steps {
                sh '''
                    ./jenkins/build/mvn.sh mvn -B -DskipTests clean package
                    ./jenkins/build/build.sh
                '''
            }

            post {
                success {
                   archiveArtifacts artifacts: 'java-app/target/*.jar', fingerprint: true
                }
            }
        }


        stage('Push') {
            steps {
                sh './jenkins/push/push.sh'
            }
        }
    }
