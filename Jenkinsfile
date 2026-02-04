pipeline {
     agent { label "agenta" }
    
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Git clone for project') {
            steps {
                echo 'Cloning the project'
                git branch: 'main', url: 'https://github.com/Pooja-gouda/Helloworld-latest.git'
            }
        }
        stage('Maven build') {
            steps {
                echo 'Build the mavem'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        }
        stage('Docker build') {
            steps {
                echo 'Docker build project'
                sh 'docker build -t travel .'
            }
        }
        stage('Login to docker hub') {
            steps {
                echo 'login to docker hub'
                sh 'docker login -u poojagoudai -p abc@12345'
            }
        }
        stage('Tag the image') {
            steps {
                echo 'Tag image'
                sh 'docker tag travel poojagoudai/travel'
            }
        }
        stage('Push the images') {
            steps {
                echo 'push image yo docker hub'
                sh 'docker push poojagoudai/travel'
            }
        }
        stage('Remove Docker conatiner') {
            steps {
                echo 'Remove Docker conatiner'
                sh 'docker stop travel_container || true'
                sh 'docker rm travel_container || true'
            }
        } 
        stage('Run docker image') {
            steps {
                echo 'Run docker image'
                sh 'docker run --name travel_container -d -p 8383:8080 poojagoudai/travel'
            }
        } 
    }
}
