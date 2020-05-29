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
                //buildName "$BUILD_NUMBER-$BRANCH-$GIT_COMMIT_SHORT"
                buildName "$BUILD_NUMBER-$GIT_COMMIT_SHORT"
                buildDescription "Executed @ ${NODE_NAME}"
            }
        }
        stage ("Build dev") {
            steps{
                build job: "/tech-dsometr/dev/tech-dsometr-build"
            }
        }
        stage ("Deploy dev") {
            steps{
                build job: "/tech-dsometr/dev/tech-dsometr-deploy"
            }
        }
        stage ("Build uat") {
            steps{
                build job: "/tech-dsometr/uat/tech-dsometr-build"
            }
        }
        stage ("Deploy uat") {
            steps{
                build job: "/tech-dsometr/uat/tech-dsometr-deploy"
            }
        }
    }
}