pipeline {
    agent any

    stages{
        stage('code scan') {
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
                sh 'ls '
            }
        }
        stage('docker login') {
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 890742578441.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('docker Image build') {
            steps{
                sh 'docker build -t qa-little-fashion:test-$BUILD_ID .'
            }
        }
        stage('docker tag') {
            steps{
                sh 'docker tag qa-little-fashion:test-$BUILD_ID 890742578441.dkr.ecr.us-east-1.amazonaws.com/qa-little-fashion:test-$BUILD_ID'
            }
        }

        stage('push image') {
            steps{
                sh 'docker push 890742578441.dkr.ecr.us-east-1.amazonaws.com/qa-little-fashion:test-$BUILD_ID'
                
            }
        }
        /*
        stage('clone') {
            steps{
                sh 'echo "clone"'
                sh 'pwd'

            }
        }
        stage('test') {
            steps{
                sh 'echo "test"'
            }
        }
        stage('create file') {
            steps{
                sh 'touch text-$BUILD_ID'
            }
        }
        */
             
    }
}
