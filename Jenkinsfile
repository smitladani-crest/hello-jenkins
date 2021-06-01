pipeline {
    agent {
        node {
            label 'agent1'
        }
    }

    tools {
        go 'go-16'
    }

    stages {
        parallel {
            stage('Build') {
                steps {
                    echo 'Building GO project...'
                    sh 'go build hellojenkins'
                    sh './hellojenkins'
                }
            }
            
            stage('Test') {
                steps {
                    echo 'Testing the program'
                    sh 'Running parallel stage'
                }
            }
        }
    }
}