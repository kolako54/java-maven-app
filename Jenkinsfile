pipeline {
    agent any
    stages {
      stage("test") {
            steps {
                echo "testing for $BRANCH_NAME started..."
                echo "testing the application..."
           }
        }
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                echo "building the application..."
            }
        }
        stage("deploy"){
            when {
                  expression {
                    BRANCH_NAME == 'master'
                 }
            }
            steps{
                echo "deploying the application"
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