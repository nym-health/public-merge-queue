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
        stage("Check if Open PR") {
            steps {
                script {
                    sh("""exit 1""")
                }
            }
        }
        stage("Run Fast") {
            steps {
                script {
                    sh("""sleep 1""")
                    sh("""exit 0""")
                }
            }
        }
        stage("Run Slow") {
            when {
                expression {
                    return env.BRANCH_NAME.contains("gh-readonly-queue/develop/pr-")
                }
            }
            steps {
                script {
                    sh("""sleep 5""")
                    sh("""exit 0""")
                }
            }
        }
    }
}
