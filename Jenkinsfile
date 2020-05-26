withFolderProperties{
    def TEST =  "${env.QWERTY}"
}

pipeline {
    agent any
    environment {
    }
    stages {
        stage ("test") {
            steps{
                echo "${TEST}"
            }

        }
    }
}