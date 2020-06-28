#!/bin/groovy
pipeline {
  agent any
  stages {
    // stage('Prepare') {
    //   steps {
    //     script {
    //       sh 'npm install yarn -g'
    //       sh 'yarn install'
    //     }
    //   }
    // }
    // stage('Test') {
    //   steps {
    //     script {
    //       sh 'yarn test'
    //     }
    //   }
    // }
    // stage('Build') {
    //   steps {
    //     script {
    //       sh 'yarn build'
    //     }
    //   }
    // }
    stage('Get JWT Token') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'Portainer', usernameVariable: 'admin', passwordVariable: 'n0br0k3rv4')]) {
              def json = """
                  {"Username": "$admin", "Password": "$n0br0k3rv4"}
              """
              def jwtResponse = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_JSON', validResponseCodes: '200', httpMode: 'POST', ignoreSslErrors: true, consoleLogResponseBody: true, requestBody: json, url: "https://portainer.testportainer.nobroker.in/api/auth"
              def jwtObject = new groovy.json.JsonSlurper().parseText(jwtResponse.getContent())
              env.JWTTOKEN = "Bearer ${jwtObject.jwt}"
          }
        }
        echo "${env.JWTTOKEN}"
      }
    }
