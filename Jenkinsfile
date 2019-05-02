node {
    def app
    stage("Checkout") {
        sh 'echo "Checkout Started ...."'
        checkout scm              
        sh 'echo "Checkout Completed ...."'
    }    
    stage("Docker build") {
        sh 'echo "build Started ...."'
        sh "docker build -f Dockerfile -t ${env.MQ_DOCKER_IMAGE_NAME}:latest ."
        sh 'echo "build Completed ...."'
    }
    stage('Docker push') {
        withCredentials([usernamePassword(credentialsId: 'cluster1-registry-credentials',
                                        usernameVariable: 'USERNAME',
                                        passwordVariable: 'PASSWORD')]) {
            sh """
            #!/bin/bash
            echo "docker push  Started ...."
            docker login -u ${USERNAME} -p ${PASSWORD} ${env.ICP_DOCKER_REG_CLUSTER1}
            docker push ${env.MQ_DOCKER_IMAGE_NAME}:latest
            echo "docker push  completed ...."
            """
        }
    }    
 }
