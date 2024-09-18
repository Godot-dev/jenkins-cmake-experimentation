pipeline {
    agent {
        docker { image 'gmao/ubuntu20-cmake'}
    }
    parameters {
        string(name: 'a', defaultValue: '9')
    }
    triggers {
        cron '@midnight'
    }
    // Add a tool configuration here...
    stages {
        stage('Build') {
            steps {
                sh 'pwd'
                sh 'mkdir build'
                sh 'cd build'
                sh 'cmake -S ..'
                sh 'make'
            }
        }
        stage('Test'){
            steps{
                sh 'pwd'
                sh 'ctest -VV > logTests.txt'
                archiveArtifacts artifacts: 'logTest.txt', followSymlinks: false
            }
        }
        stage('Deploy'){
            steps{
                sh 'pwd'
                sh "./Tutorial ${params.a} > log.txt"
                archiveArtifacts artifacts: 'log.txt', followSymlinks: false
            }
        }
    }
}