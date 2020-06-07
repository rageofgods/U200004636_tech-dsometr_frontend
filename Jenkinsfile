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
                build job: "./build/dev/build", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.build_dev
                }
            }
        }
        stage ("Deploy dev") {
            steps{
                build job: "./deploy/dev/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.deploy_dev
                }
            }
        }
        stage ("Build trust") {
            steps{
                build job: "./build/trust/build", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.build_trust
                }
            }
        }
        stage ("Deploy uat") {
            steps{
                build job: "./deploy/uat/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.deploy_uat
                }
            }
        }
        stage ("Deploy PreProd") {
            steps{
                build job: "./deploy/preprod/deploy", parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "$BRANCH"]]
            }
            when {
                expression {
                    return params.deploy_preprod
                }
            }
        }
    }
}