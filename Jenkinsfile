pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
    }

    environment {
        GIT_COMMIT_SHORT = sh(
            script: "printf \$(git rev-parse --short ${GIT_COMMIT})",
            returnStdout: true
        )
    }

    stages {
        stage("Set build name") {
            steps {
                // use name of the patchset as the build name
                script {
                    if ("${params.BRANCH}" == 'null'){
                        buildName "$BUILD_NUMBER-$GIT_COMMIT_SHORT"
                    }
                    else {
                        buildName "$BUILD_NUMBER-${params.BRANCH}-$GIT_COMMIT_SHORT"
                    }
                }
                //buildName "$BUILD_NUMBER-$GIT_COMMIT_SHORT"
                buildDescription "Executed @ ${NODE_NAME}"
            }
        }
        stage ("Build dev") {
            steps{
                build job: "./dev/build", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.dev
                }
            }
        }
        stage ("Deploy dev") {
            steps{
                build job: "./dev/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.dev
                }
            }
        }
        stage ("Build uat") {
            steps{
                build job: "./uat/build", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.uat
                }
            }
        }
        stage ("Deploy uat") {
            steps{
                build job: "./uat/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.uat
                }
            }
        }
        stage ("Build PreProd") {
            steps{
                build job: "./preprod/build", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.preprod
                }
            }
        }
        stage ("Deploy PreProd") {
            steps{
                build job: "./preprod/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.preprod
                }
            }
        }
    }
}