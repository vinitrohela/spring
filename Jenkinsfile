#!/usr/bin/env groovy

node {
  stage "Git Checkout vkunr"
  checkout scm

  stage "Assemble vkunr"
    sh "./gradlew assemble"
    withCredentials([
      [
      $class          : 'UsernamePasswordMultiBinding',
      credentialsId   : 'cac89846-cfae-4828-a49c-5f4e666201ab',
      passwordVariable: 'CF_PASSWORD',
      usernameVariable: 'CF_USERNAME'
      ]]) {

       stage "Deploy"
       sh "cf login -a api.cf.nonprod-mpn.ro11.allstate.com -u ${CF_USERNAME} -p ${CF_PASSWORD}; cf target -o IS-COMPOZED-ACCELERATOR -s INT; cf push"
      }
}
