pipeline {
    agent any

    tools {
        jdk 'java21'
        maven 'maven'
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'master', url: 'git@github.com:adarsh1104/netflix_project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package WAR') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Upload to S3') {
            steps {
                s3Upload consoleLogLevel: 'INFO',
                    entries: [[
                        bucket: 'artifactbucketfornetflixapp',
                        sourceFile: 'target/NETFLIX-1.2.2.war',
                        selectedRegion: 'ap-south-1',
                        storageClass: 'STANDARD'
                    ]],
                    profileName: 'raham'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment stage"
            }
        }
    }
}

