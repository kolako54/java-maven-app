#!/usr/bin/env groovy
// if i have a variable definition after this Library, we shouldn't put _ beside that, otherwise we should put.
@Library('jenkins-shared-library')
def gv
pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
      stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
      }
      stage("build jar") {
            steps {
                script {
                    buildJar()
                }
           }
        }
        stage("build image") {
            steps {
                script {
                    buildImage "kolako54/my-maven-repo:jma-3.0"
                }
            }
        }
        stage("deploy"){

            steps{
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
// pipeline {
//     agent any
//     tools {
//         maven 'Maven'
//     }
//     stages {
//         stage("build jar"){
//             steps {
//                 echo "building the application..."
//                 sh "mvn package"
//             }
//         }
//         stage("build image"){
//             steps {
//                 script {
//                     echo "building the docker image..."
//                     withCredentials([
//                         usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')
//                     ]){
//                         sh 'docker build -t kolako54/my-maven-repo:jma-2.0 .'
//                         sh "echo $PASS | docker login -u $USER --password-stdin"
//                         sh "docker push kolako54/my-maven-repo:jma-2.0"
//                     }
//                 }
//             }
//         }
//         stage("deploy"){
//             steps{
//                 echo "deploying the application"
//             }
//         }
//     }
// }