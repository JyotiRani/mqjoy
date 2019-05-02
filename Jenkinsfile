node {
    def app
    stage("Checkout") {
        sh 'echo "Checkout Started ...."'
        checkout scm
        sh "cp -r ./* ./"        
        sh 'echo "Checkout Completed ...."'
    }    
    stage("Docker build") {
        sh 'echo "build Started ...."'
        sh "docker build -f Dockerfile -t ${env.DOCKER_IMAGE_NAME_MQ}:latest ."
        sh 'echo "build Completed ...."'
    }
 }
