pipeline {
    agent any
    stages {
        stage('Do stuff') {
            steps {
                echo "Hello hello"
                //error ("ouch")
                script {
                    currentBuild.result = hudson.model.Result.UNSTABLE.toString()
                }
            }
        }
    }
  post {
    success {
        setBuildStatus("Build asg succeeded", "SUCCESS");
    }
    unstable {
        setBuildStatus("Build asg unstable", "pending");
    }
    failure {
        setBuildStatus("Build asg failed", "FAILURE");
    }
  }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status-asg"],
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
