def upload_artifacts

pipeline {
    agent {
        node {
            label 'master'
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
        
        stage('Decide to store artifacts') {
            steps {
                script {
                    upload_artifacts = input message: "Would you like to upload artifacts to s3 bucket and deploy the build?",
                    parameters: [
                        booleanParam(name: 'UPLOAD_ARTIFACTS', defaultValue: true, description: 'Check if you would like to upload the artifacts to s3 bucket else uncheck it'),
                        choice(name: 'DEPLOY_BUILD', choices: 'no\nyes', description: 'Choose "yes" if you want to deploy this build')
                    ]
                }
            }
        }

        stage('Store-artifacts') {

            when { 
                expression { 
                    return upload_artifacts.UPLOAD_ARTIFACTS
                }
            }

            steps {
                echo "uploadArtifacts: ${upload_artifacts.UPLOAD_ARTIFACTS}"
                echo "deploy build: ${upload_artifacts.DEPLOY_BUILD}"
                echo "*************************"
                echo "List of objects in the bucket"
                sh "aws s3 ls s3://learn-jenkins-bucket-to-store-artifacts"
                echo "Uploading artifacts..."
                sh "aws s3 cp hellojenkins s3://learn-jenkins-bucket-to-store-artifacts"
            }
        }
    }
}