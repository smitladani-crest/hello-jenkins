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
            steps {
                echo 'Building GO project...'
                sh 'go build hellojenkins'
                sh './hellojenkins'
            }
        }
        
        stage('Store-artifacts') {
            input {
                message "Would you like to upload artifacts to s3 bucket?"
                parameters {
                    booleanParam(name: 'uploadArtifacts', defaultValue: true, description: 'Check if you would like to upload the artifacts to s3 bucket else uncheck it')
                }
            }

            // when {
            //     equals expected: true, actual: params.uploadArtifacts
            // }

            steps {
                echo "uploadArtifacts: ${params.uploadArtifacts}"
                echo '*************************'
                echo 'Uploading artifacts'
            }
        }
    }
}