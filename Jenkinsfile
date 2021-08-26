pipeline {

    agent any
    sdf
    environment {
        PASS = credentials('registry-pass') 
    }sdf

    stages {
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
