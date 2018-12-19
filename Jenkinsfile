pipeline {
    agent any
    environment {
        PMD_RULESET_FILE = "./pmd-apex-ruleset.xml"
        PMD_RESULTS_FILE = "./pmd.xml"
    }
    stages {
        stage('Run code analysis') {
            steps {
                dir("/api-poc/api-people") {
                    sh "pmd -dir . -format html -rulesets ${env.PMD_RULESET_FILE} -reportfile ${env.PMD_RESULTS_FILE} -failOnViolation false"
                }
            }
        }
    }
}
