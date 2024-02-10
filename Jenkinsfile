pipeline {
    agent {
        label "jenkins-slave"
    }
    tools {
        jdk "jdk17"
        maven "maven3"
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
    }
}
