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
                    String buildCause = currentBuild.getBuildCauses()[0]["shortDescription"].toString()
                    echo("$buildCause")
//                  String inputString = 'gh-readonly-queue/develop/pr-90-98b320b705e10a5058ba7d95a275e5df7354e82e'
                    def prNumber = buildCause =~ /pr-\d+/
                    if (prNumber) {
//                      println "PR Number: ${prNumber[0]}"

                        prNumberString=prNumber[0].toString()
                        println "PR Number: ${prNumberString}"
                        scmUtils.commentPr(repo: "public-merge-queue", prNumber: prNumberString, comment: "hi omer")
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
