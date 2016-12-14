#!/usr/bin/env groovy
def docker_registry


node {
   docker_registry = env.DOCKER_REGISTRY
   checkout scm
}

docker.image(docker_registry + "/compozed/ci-base:0.6").inside() {
    env.GRADLE_USER_HOME = "."

    stage "Assemble building ..."
      sh "./gradlew assemble"

    withCredentials([
        [
        $class          : 'UsernamePasswordMultiBinding',
        credentialsId   : 'ca9db6c7-b7b4-4c98-a287-31117a4a827f',
        passwordVariable: 'CF_PASSWORD',
        usernameVariable: 'CF_USERNAME'
        ]]) {

         stage "Deploy..."
         sh "cf login -a api.cf.nonprod-mpn.ro11.allstate.com -u ${CF_USERNAME} -p ${CF_PASSWORD} --skip-ssl-validation; cf target -o IS-COMPOZED-ACCELERATOR -s INT; cf push"
        }
}
