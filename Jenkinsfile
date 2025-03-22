pipeline{
    agent any

    environment {
        GIT_CREDENTIALID = 'github-credential'
        DOCKER_HUB_USER = 'sureshk89' 
        DOCKER_HUB_PASSWORD = 'Greengrass@89'
        IMAGE_NAME = 'sureshk89/python-jenkin'
    }
    stages{
        stage('Clone Repository'){
            steps {
                script{
                    checkout ([$class: 'GitSCM', 
                    branches:[[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Suresh8904/Python-Jenkin.git',
                        credentialsId: GIT_CREDENTIALID
                    ]]
                    ])
                }
            }
        }
         stage('Docker Build'){
            steps {
                script {
                    bat 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Docker login'){
            steps {
                script {
                   bat 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USER --password-stdin' 
                }
            }
        }

        stage('Docker Push'){
            steps {
                script {
                   bat 'docker push $IMAGE_NAME' 
                }
            }
        }
    }
}