#!/usr/bin/env groovy

node {
  stage "Git Checkout vkunr"
  checkout scm

  stage "Assemble vkunr"
    sh "./gradlew assemble"
}
