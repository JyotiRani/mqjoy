node {
    def app
    stage("Docker build") {
        sh 'echo "build Started ...."'
        sh "docker build -f Dockerfile -t ${env.DOCKER_IMAGE_NAME_MQ}:latest ."
        sh 'echo "build Completed ...."'
    }
 }
