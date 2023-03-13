library "nym-shared-library@$develop"

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
            failFast false
            parallel {
                stage("Run Fast AU Pytest") {
                    steps {
                        script {
                            fastau = build(job: "Sandbox/Berger/fast-au-pytest/develop", wait: true, propagate: false)
                            url = fastau.getAbsoluteUrl()
                            echo "$url"
                        }
                    }
                }
                stage("Run Fast Parrot Pytest") {
                    steps {
                        build(job: "Sandbox/Berger/fast-parrot-pytest/develop", wait: true, propagate: true)
                    }
                }
            }
        }
    }
}
