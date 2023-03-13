library "nym-shared-library@develop"

import java.util.regex.Pattern

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
                    sh("""sleep 5""")
                }
            }
        }
        stage("Notify GitHub") {
            steps {
                script {
                    def input = currentBuild.getBuildCauses()[0]["shortDescription"].toString()
                    def pattern = Pattern.compile("(?i)PR-\\d+")
                    def matcher = pattern.matcher(input)

                    echo("$input")

                    if (matcher.find()) {
                        prNumber = matcher.group()
                        println "PR Number: ${prNumber}"
                        scmUtils.commentPr(repo: "public-merge-queue", prNumber: prNumber, comment: "hi omer")
                    } else {
                        println "No PR number found in input string"
                    }
                }
            }
        }
    }
}

//pipeline {
//    agent { label 'jenkins-small' }
//    options {
//        timeout(time: 2, unit: "HOURS")
//        buildDiscarder(logRotator(artifactDaysToKeepStr: "30",
//                                  artifactNumToKeepStr: "",
//                                  daysToKeepStr: "30",
//                                  numToKeepStr: ""))
//    }
//    stages {
//        stage("Run Fake Pytest") {
//            steps {
//                script {
//                    echo("""Pytest I choose you 🧪""")
//                    sh("""sleep 5""")
//                }
//            }
//        }
//    }
//}
