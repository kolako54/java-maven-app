#!/usr/bin/env groovy
// if i have a variable definition after this Library, we shouldn't put _ beside that, otherwise we should put.
// this is for globally
// @Library('jenkins-shared-library')
// for per each of project
library identifier: 'jenkins-shared-library@main', retriever: modernSCM(
    [
        $class: 'GitSCMSource',
        remote: 'https://github.com/kolako54/jenkins-shared-library.git',
        credentialsId: 'github-credentials'
    ]
)
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
        stage("build and push imagess") {
            steps {
                script {
                    buildImage "kolako54/my-maven-repo:jma-3.0"
                    dockerLogin()
                    dockerPush "kolako54/my-maven-repo:jma-3.0"

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