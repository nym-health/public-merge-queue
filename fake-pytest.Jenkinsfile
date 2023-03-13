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
        stage("Run Fake Pytest") {
            steps {
                script {
                    echo("""Pytest I choose you 🧪""")
                    sh("""sleep 10""")
                }
            }
        }
    }
}
