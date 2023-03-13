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
        stage("Sleep Slow") {
            steps {
                script {
                    sh("""sleep 5""")
                }
            }
        }
        stage("Run Pytest") {
            steps {
                build(job: "Sandbox/Berger/Fake Pytest/develop", wait: true, propagate: true)
            }
        }
        stage("Sleep Slow") {
            steps {
                script {
                    sh("""exit 55""")
                }
            }
        }
    }
}

