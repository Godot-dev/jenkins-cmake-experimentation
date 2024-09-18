pipeline {
    agent {
        docker { image 'conanio/gcc10'
                 args ''
        }

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
                sh "cmake -S . -B ."
                sh 'make'
            }
        }
        stage('Test'){
            steps{
                sh 'pwd'
                sh 'ctest -VV > logTests.txt'
                archiveArtifacts artifacts: 'logTests.txt', followSymlinks: false
            }
        }
        stage('Deploy'){
            steps{
                sh 'pwd'
                sh "./Tutorial ${params.a} > logs.txt"
                archiveArtifacts artifacts: 'logs.txt', followSymlinks: false
            }
        }
    }
}