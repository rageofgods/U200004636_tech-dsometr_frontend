withFolderProperties{
    def TEST =  "${env.QWERTY}"
}

pipeline {
    agent {
        any
    }
    environment {
    }
    stages {
        stage {
            steps{
                echo "${TEST}"
            }

        }
    }
}