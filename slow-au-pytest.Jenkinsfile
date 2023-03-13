pipeline {
    agent { label 'jenkins-small' }
    options {
        timeout(time: 2, unit: "HOURS")
        buildDiscarder(logRotator(artifactDaysToKeepStr: "30",
                                  artifactNumToKeepStr: "",
                                  daysToKeepStr: "30",
                                  numToKeepStr: ""))
    }
    stages {
        stage("Run slow") {
            steps {
                script {
                    sh("""sleep 10""")
                    sh("""exit 0""")
                }
            }
        }
    }
}
