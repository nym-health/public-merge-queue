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
        stage("Run Tests") {
            steps {
                script {
                    echo("=== START ===")
                    sh("sleep 10")
                    echo("=== DONE ===")
                }
            }
        }
    }
}
