pipeline {
    agent none

    stages {
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