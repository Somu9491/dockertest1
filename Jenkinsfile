pipeline {
    environment {
        registry = 'somu9491/devops1'
        registryCredential = 'dockerhub_id'
      /*  dockerSwarmManager = '10.40.1.26:2375 '    */
         dockerhost = '10.40.1.26'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/Somu9491/dockertest1.git'
            }
        }
        stage('Building Docker image') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/pipeline2 - dockertest1'
                sh 'cp /var/lib/jenkins/workspace/pipeline2 - dockertest1/*/var/lib/jenkins/workspace/pipeline2'
                    sh 'docker build -t somu9491/pipelinetest:v$BUILD_NUMBER'
                }
            }
        }
        stage('Push Image To DockerHUB') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:v$BUILD_NUMBER"
            }
        }
   /*     stage('Deploying to Docker Swarm') {
            steps {
                sh "docker -H tcp://$dockerSwarmManager service rm testing1 || true"
                sh "docker -H tcp://$dockerSwarmManager service create --name testing1 -p 8100:80 $registry:v$BUILD_NUMBER"
            }
        }
        stage('Verifying The Deployment') {
            steps {
                sh 'curl http://$dockerhost:8100 || exit 1'
                }
        }  */
    }
}
