def pmdpath = ""
pipeline {
    agent any
    environment {
        PMD_RULESET_FILE = "./pmd-apex-ruleset.xml"
        PMD_RESULTS_FILE = "./pmd.html"
    }
    stages {
        stage('Get tools') {
            steps {
                script {
                    def pmdtool = tool (
                        name: 'pmd',
                        type: 'com.cloudbees.jenkins.plugins.customtools.CustomTool'
                    )
                    pmdpath = "${pmdtool}/run.sh pmd"
                }
            }
        }
        stage('Run code analysis') {
            steps {
                dir("/api-poc/api-people") {
                    sh "${pmdpath} -dir . -format xslt -property xsltFilename=pmd-report.xsl -rulesets ${env.PMD_RULESET_FILE} -reportfile ${env.PMD_RESULTS_FILE} -failOnViolation false"
                    archiveArtifacts (
                        artifacts: "pmd.html"
                    )
                    archiveArtifacts (
                        artifacts: "pmd-report.css"
                    )
                }
            }
        }
    }
}
