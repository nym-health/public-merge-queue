pipeline {
    agent { label 'jenkins-small' }
    options {
        timeout(time: 2, unit: "HOURS")
        buildDiscarder(logRotator(artifactDaysToKeepStr: "30",
                                  artifactNumToKeepStr: "",
                                  daysToKeepStr: "30",
                                  numToKeepStr: ""))
        disableConcurrentBuilds abortPrevious: true
    }
    stages {
        stage("Run Fast") {
            steps {
                script {
                    sh("""sleep 1""")
                    sh("""exit 0""")
                }
            }
        }
        stage("Run Fast Tests") {
            steps {
                script {
                    sh("""sleep 1""")
                    sh("""exit 0""")
                }
            }
        }
    }
}
