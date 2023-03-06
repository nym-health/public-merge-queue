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
                    sh("""
                        # Replace with your own values
                        owner="nym-health"
                        repo="public-merge-queue"
                        branch="\$env.BRANCH_NAME"
                        token=""
    
                        # Construct the API endpoint URL
                        url="https://api.github.com/repos/${owner}/${repo}/pulls"
    
                        # Set the query parameters to filter by the branch name
                        params="state=open&head=${owner}:${branch}"
    
                        # Set the authentication headers using your PAT
                        headers="Authorization: token ${token}"
    
                        # Send the API request
                        response=\$(curl -sSL -H "${headers}" "${url}?${params}")
    
                        # Check if the response contains any pull requests
                        if [[ \$(echo "${response}" | jq length) -gt 0 ]]; then
                            echo "There are open pull requests for ${branch}"
                            exit 0
                        else
                            echo "No open pull requests for ${branch}"
                            exit 1
                        fi
                    """)
                    sh("""exit 0""")
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
            steps {
                script {
                    if(env.BRANCH_NAME.contains("gh-readonly-queue/develop/pr-")) {
                        echo("=== RUN SLOW ===")
                        sh("""sleep 5""")
                        sh("""exit 5""")
                    } else {
                        echo("=== DO NOT RUN SLOW ===")
                    }
                }
            }
        }
    }
}
