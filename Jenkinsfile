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
                sh 'mkdir /tmp/build'
                dir('/tmp/build'){
                    sh 'pwd'
                    sh "cmake -S ${env.WORKSPACE}/jenkins-cmake-experimentation -B ."
                    sh 'make'
                }
            }
        }
        stage('Test'){
            steps{
                sh 'pwd'
                dir('/tmp/build'){
                    sh 'pwd'
                    sh 'ctest -VV > logTests.txt'
                    archiveArtifacts artifacts: 'logTest.txt', followSymlinks: false
                }
            }
        }
        stage('Deploy'){
            steps{
                sh 'pwd'
                dir("${env.WORKSPACE}/jenkins-cmake-experimentation@tmp/build"){
                    sh "./Tutorial ${params.a} > log.txt"
                    archiveArtifacts artifacts: 'log.txt', followSymlinks: false
                }
            }
        }
    }
}