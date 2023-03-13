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
        stage('Check for upstream build') {
            when {
                expression {
                    currentBuild.causes.find { it.getClass().getName().equals("hudson.model.Cause$UpstreamCause") }
                }
            }
            steps {
                script {
                    def upstreamBuild = currentBuild.causes.find { it.getClass().getName().equals("hudson.model.Cause$UpstreamCause") }
                    echo "I was triggered by another build ${upstreamBuild.upstreamProject} #${upstreamBuild.upstreamBuild}"
                }
            }
        }

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
