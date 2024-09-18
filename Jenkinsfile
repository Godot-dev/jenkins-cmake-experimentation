pipeline {
    agent {
        docker { image 'godot-cmake'}

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
                sh 'ctest --output-junit logTests.xml'
            }
        }
        stage('Deploy'){
            steps{
                sh 'pwd'
                sh "./Tutorial ${params.a} > logs.txt"
                archiveArtifacts artifacts: 'logs.txt', followSymlinks: false
            }
        }
        post {
            always {
                junit allowEmptyResults: true, testResults: 'logTests.xml'
            }
        }
    }
}