pipeline {
    agent any

    stages {
        stage ("Build dev") {
            steps{
                build job: "/tech-dsometr/dev/tech-dsometr-build"
            }
        }
        //stage ("Deploy dev") {
        //    steps{
        //        build job: "/tech-dsometr/devtech-dsometr-deploy"
        //    }
        //}
    }
}