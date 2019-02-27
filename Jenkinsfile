node {
    stage("SCM checkout"){
        git credentialsId: 'git_cred', url: 'https://github.com/silemilan/test.git'
    }

    stage("Build docker image") {
        sh "docker-compose -f docker-compose-build.yml build"
    }

    stage("Push docker image") {
        withCredentials([string(credentialsId: 'dockerhub1', variable: 'dockerHubPass')]) {
            sh "docker login -u silemilan -p ${dockerHubPass}"
            
        }
        sh "docker push silemilan/docker_image:$BUILD_TAG"
    }
    stage("deploy and run image") {
        def dockerRun="docker run -d -name probadocker silemilan/dockerimage:$BUILD_TAG"
        sshagent(['remote_host']) {
            sh "ssh -o StrictHostKeyChecking=no centos_user@remote_host ${dockerRun}"
        }
    }

}