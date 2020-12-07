pipeline {
    agent any

    stages {
        stage("Build") {
            steps {
                echo "Some code compilation here..."
                sh "chmod +x gradlew && ./gradlew build"
            }
        }

        stage("Test") {
            steps {
                echo "Some tests execution here..."
            }
        }
    }
}
