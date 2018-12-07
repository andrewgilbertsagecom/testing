pipeline {
    agent any
    stages {
        stage('Do stuff') {
            steps {
                echo "Hello bob"
            }
        }
    }
  post {
    success {
        setBuildStatus("Build asg succeeded", "SUCCESS");
    }
    failure {
        setBuildStatus("Build asg failed", "FAILURE");
    }
  }
}

void setBuildStatus(String message, String state) {
  step([
      $class: "GitHubCommitStatusSetter",
      errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
      statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}
