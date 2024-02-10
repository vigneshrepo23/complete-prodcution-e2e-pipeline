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
    }
}
