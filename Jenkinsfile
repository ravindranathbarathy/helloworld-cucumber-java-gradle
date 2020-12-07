nodeLabel = "gradle"

pipeline {
    agent {
        kubernetes { 
            label nodeLabel
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    worker: ${nodeLabel}
spec:
  containers:
  - name: docker
    image: docker:19.03.1
    command:
    - sleep
    args:
    - 99d
    env:
      - name: DOCKER_HOST
        value: tcp://localhost:2375
  - name: docker-daemon
    image: docker:19.03.1-dind
    securityContext:
      privileged: true
    env:
      - name: DOCKER_TLS_CERTDIR
        value: ""
            """
        
        }
    }
    stages {
        stage("Build") {
            agent { docker { image 'gradle' }
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
