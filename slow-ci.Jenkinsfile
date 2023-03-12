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
        stage("Run Slow") {
            steps {
                script {
                  sh("""sleep 60""")
                }
            }
        }
        stage("Run Slow Tests") {
            failFast false
            parallel {
                stage("Run Slow AU Pytest") {
                    steps {
                        build(job: "Sandbox/Berger/slow-au-pytest/develop", wait: true, propagate: true)
                    }
                }
                stage("Run Slow Parrot Pytest") {
                    steps {
                        build(job: "Sandbox/Berger/slow-parrot-pytest/develop", wait: true, propagate: true)
                    }
                }
            }
        }
    }
}

