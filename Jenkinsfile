// pipeline {
//     agent any
//     stages {
//         stage("build"){
//             steps {
//                 echo "building the application..."
//             }
//         }
//         stage("test"){
//             steps {
//                 echo "testing the application..."
//             }
//         }
//         stage("deploy"){
//             steps{
//                 echo "deploying the application"
//             }
//         }
//     }
// }

// CODE_CHANGES = getGitChanges()
def gv
pipeline {
    agent any
    environment{
        // create env var
        NEW_VERSION = '1.3.0'
        // this is method or function that b inds credeintials to env variable, i should just install plugin called "Credentials Binding" in junkins ui. (by default it is enable)
        // parameter will get credential id.
//         SERVER_CREDENTIALS = credentials('')
    }

    // parameter can be used as a configuration
    parameters {
        // type of parameter is string, name of parameter is VERSION
        string(name: 'VERSIONString', defaultValue: '', description: 'select version to deploy on prod')
        // instead of having to enter input a version name, you can have predefined a choices of different versions that you can actually choose from.
        choice(name: 'VERSIONChoice', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        // you want to skip a certain stage.
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    // provide preinstalled build tools
//     tools {
//         maven 'Maven'
//         gradle
//     }
    stages {
     stage("init"){
                steps {
                    script {
                        gv = load "script.groovy"
                    }
                }
            }
        stage("build"){
//             when{
//                 expression {
//                     CODE_CHANGES == true
//                 }
//             }
            steps {
                echo "building the application..."
                echo "building version ${NEW_VERSION}"
//                 sh "mvn install"
            }
        }
        stage("test"){
            when{
                expression {
                    // if branch name was in dev or branch_name was master, then perform the steps
//                     BRANCH_NAME == 'dev' || BRANCH_NAME = 'master'
                    // if executeTests parameter was true, then perform this stage.
                    //? params.executeTests == true
                    // or just:
                    params.executeTests
                }
            }
            steps {
                echo "testing the application..."
            }
        }
        stage("deploy"){
//         input{
//             message "Select the environment to deploy to"
//             ok "Done"
//             parameters {
//                 choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: '')
//             }
//         }
            steps {

                echo "deploying the application"
                // that is a function that let me get password and username individually,
                // what usernameVariable do, is take the username and store it on the USER
                // withCredentials([
                //     usernamePassword(credentials: 'server-credentials')
                //     usernameVariable: USER, passwordVariable: PWD
                //     ]) {
                //         sh "some script ${USER} ${PWD}"
                // }

//                 echo "deploying version ${params.VERSIONChoice}"
//                 echo "deploying to ${ENV}"
                script {
                 //* to assign input parameter that user enter in, into a variable
                     env.ENV = input message: "Select the environment to deploy to",
                     ok: "Done",
                     parameters: [choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: '')]
                     echo "Deploying to ${ENV}"
                     gv.deployApp()
                }
            }
        }
    }
//     post {
//         failure {}
//         always {}
//         success {}
//     }
}