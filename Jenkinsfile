pipeline {
    agent {
        docker { image 'conanio/gcc10'}
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
                dir("${env.WORKSPACE}/jenkins-cmake-experimentation/build")
                sh 'ctest -VV > logTests.txt'
                archiveArtifacts artifacts: 'logTest.txt', followSymlinks: false
            }
        }
        stage('Deploy'){
            steps{
                sh 'pwd'
                dir("${env.WORKSPACE}/jenkins-cmake-experimentation/build")
                sh "./Tutorial ${params.a} > log.txt"
                archiveArtifacts artifacts: 'log.txt', followSymlinks: false
            }
        }
    }
}