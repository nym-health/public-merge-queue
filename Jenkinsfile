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
        stage("Start") {
            steps {
                script {
                    echo("=== START ===")
                }
            }
        }
        stage("Sleep") {
            steps {
                script {
                    sh("sleep 10")
                }
            }
        }
        stage("Finish") {
            steps {
                script {
                    echo("=== Finish ===")
                }
            }
        }
    }
}
