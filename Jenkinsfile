pipeline {
    agent any

    stages {
        stage ("1.clean workspace") {
            steps {
                cleanWs()
            }
        }
        stage('2. Git Checkout'){
            steps {
                git branch: 'master', changelog: false, poll: false, url: 'https://github.com/ebsenthil/senthiltest.git'
            }
        }
        
        stage ("3. Docker Build") {
            steps {
                sh 'docker build -t 1stnginx .'
            }
        }
        stage ("4.Tag & Push to DockerHub") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'Docker') {
                        sh "docker tag 1stnginx ebsenthil/1stnginx:latest"
                        sh "docker push ebsenthil/1stnginx:latest"
                    }
                }
            }
        }
        
        stage ("5.Deploy to Conatiner") {
            steps {
                sh 'docker run -d --name 1stnginx -p 80:80 ebsenthil/1stnginx:latest'
            }
        }
    }}
        
            

