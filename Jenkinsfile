pipeline {
    agent {
        label "jenkins-slave"
    }
    tools {
        jdk "jdk17"
        maven "maven3"
    }

    environment {
        APP_NAME = "test-project"
        RELEASE = "1.0.0"
        DOCKER_USERNAME = "vigneshrepo23"
        DOCKER_PASS = "dockerpass"
        IMAGE_NAME = "${DOCKER_USERNAME}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}" + "${BUILD_NO}"
    }

    stages {
        stage ("cleanWs"){
            steps {
                cleanWs()
            }
        } 

        stage ("git checkout") {
            steps {
                git branch: 'main', credentialsId: 'gitcred', url: 'https://github.com/vigneshrepo23/complete-prodcution-e2e-pipeline'
            }
        }

        stage ("build") {
            steps {
                sh "mvn clean package"
            }
        }

        stage ("test") {
            steps {
                sh "mvn test"
            }
        }

        stage ("sonarqube analysis") {
            steps {
                withSonarQubeEnv('mysonar') {
                sh "mvn sonar:sonar"
               }  
            } 
        }

        stage ("quality gates") {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                waitForQualityGate abortPipeline: true
               }
            }
        }

        stage ("docker push") {
            steps {
                docker.withRegistry{'https://registry.hub.docker.com', DOCKER_PASS} {
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
    }
}
