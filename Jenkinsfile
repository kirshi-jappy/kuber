pipeline {
    agent any

    environment {
        TMPDIR = '/tmp/jenkins_tmp'
    }

    stages {
        stage('Setup Temp Dir') {
            steps {
                sh '''
                mkdir -p $TMPDIR
                chmod 777 $TMPDIR
                echo "Temp directory set to $TMPDIR"
                '''
            }
        }
        // Your existing stages follow...
        stage('Clean Deployment Directory') {
            steps {
                sh 'sudo rm -rf /home/ubuntu/CommunityCronJob/*'
            }
        }
        stage('Copy Project Files') {
            steps {
                sh 'sudo cp -r . /home/ubuntu/CommunityCronJob'
                sh 'pwd'
            }
        }
        stage('Docker Compose Build & Up') {
            steps {
                dir('/home/ubuntu') {
                    sh 'sudo docker images'
                    sh 'sudo docker ps'
                    sh 'sudo docker-compose build'
                    sh 'sudo docker-compose up -d'
                    sh 'sudo docker ps'
                }
            }
        }
    }
}
