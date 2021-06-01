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
        
        stage('Build') {

            agent {
                node {
                    label 'master'
                }
            }
            
            steps {
                echo 'Building GO project...'
                sh 'go build hellojenkins'
                sh './hellojenkins'
                sh 'sleep 10'
            }
        }
            
        stage('Test') {

            parallel {
                
                stage('Parallel-1') {
                    steps {
                        echo 'Parallel-1 stage inside the test stage'
                        sh 'sleep 5'
                    }
                }

                stage('Parallel-2') {
                    steps {
                        echo 'Parallel-2 stage inside the test stage'
                        sh 'sleep 3'
                    }
                }
            }
        }
    }
}