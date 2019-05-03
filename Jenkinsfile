node {
    def app
    stage("Checkout") {
        sh 'echo "Checkout Started ...."'
        checkout scm              
        sh 'echo "Checkout Completed ...."'
    }    
    stage("Docker build") {
        sh 'echo "build Started ...."'
        sh "docker build -f Dockerfile -t ${env.ICP_DOCKER_REG_CLUSTER1}/hcl-mq/${env.MQ_DOCKER_IMAGE_NAME}:latest ."
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
            docker push ${env.ICP_DOCKER_REG_CLUSTER1}/hcl-mq/${env.MQ_DOCKER_IMAGE_NAME}:latest
            echo "docker push  completed ...."
            """
        }
    }
     stage("Deploy mq Docker Image") {
         withCredentials([kubeconfigContent(credentialsId: 'CLUSTER1_KUBE_CONFIG', variable: 'KUBECONFIG_CONTENT')]) {
            sh """
             echo "$KUBECONFIG_CONTENT" > kubeconfig && cat kubeconfig && rm kubeconfig
             kubectl get pods
            """ 
        }
        //withKubeConfig([credentialsId: 'CLUSTER1_KUBE_CONFIG', serverUrl: 'https://9.121.242.180']) { 
          //  sh """
            //#!/bin/bash
            //echo "Deploy Started ...."
            //kubectl get pods
            
            //echo "Deploy Completed ...."
            //"""
        //}
    }   
 }
