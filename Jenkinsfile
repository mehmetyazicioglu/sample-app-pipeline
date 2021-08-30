#!/usr/bin/env groovy
pipeline {
  agent any
   tools { 
        maven 'maven' 
    }
  stages {
    stage("Build"){
     agent { docker 'maven:latest' }
      steps {
	sh 'mvn clean package -DskipTests=true'
      }
    }
    stage("Testing") {
      parallel {
        stage("Unit Tests") {
          agent { docker 'openjdk:7-jdk-alpine' }
          steps {
            sh 'mvn surefire:test -fae'
          }
        }
        stage("Functional Tests") {
          agent { docker 'openjdk:8-jdk-alpine' }
          steps {
            sh 'java -version'
          }
        }
        stage("Integration Tests") {
          steps {
            sh 'java -version'
          }
        }
      }
    }

    stage("Deploy") {
      steps {
        echo "Deploy!"
      }
    }
  }
}

