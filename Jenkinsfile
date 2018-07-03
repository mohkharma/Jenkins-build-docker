node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("mkharma/jenkins-build-docker")
    }

     /* We test our image with a simple smoke test:
         * Run a curl inside the newly-build Docker image */

    /*
    stage('Test image') {
       
        app.inside {
            sh 'curl http://localhost:8000 || exit 1'
        }
    }
    */
stage "tag docker image"
    
        sh "docker tag mkharma/jenkins-build-docker localhost:5000/jenkins-build-docker:latest"
        
    
        }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
      //  docker.withRegistry('https://registry.hub.docker.com', 'docker.hub.credential') {
     // docker push localhost:5000/local.io/docker-java
      sh "docker login -p KeVGpY24nvZB1wwB2DaavikbAJeWL5NiT41ZpnIGHwk -u unused docker-registry-default.assistahealth.com"
     sh "docker push docker-registry-default.assistahealth.com/mkharma/jenkins-build-docker:latest"
        
      //  docker.withRegistry('https://docker-registry-default.assistahealth.com', 'openshift.onpremise.credential') {
       //     app.push("${env.BUILD_NUMBER}")
       //     app.push("latest")
       // }
    }
}
