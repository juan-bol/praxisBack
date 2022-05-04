pipeline {
    agent any

    options {
        timeout(time: 3, unit: 'MINUTES')
    }

    environment {
        ARTIFACT_ID = "juan2203/backendpraxis2022"
    }

    stages {
        stage("Build Backend Docker Image"){
            steps{
                script {
                    latestImage = docker.build("${env.ARTIFACT_ID}:latest")
                }
            }
        }

        // stage('Run UI Tests') {
        //     steps {
        //         sh "docker run -p 3030:3030 ${env.ARTIFACT_ID} npm test"
        //     }
        // }

        stage("Publish Docker Image in DockerHub"){
            steps {
                script {
                    docker.withRegistry("", "dockerhub_id") {
                        latestImage.push()
                    }
                }
            }   
        }

    }  


}




