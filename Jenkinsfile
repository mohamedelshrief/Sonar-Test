node {
  stage('SCM') {
    git 'https://github.com/mohamedelshrief/Sonar-Test.git'
  }

  stage('SonarQube analysis') {
    def scannerHome = tool 'SonarScanner 4.0'
    withSonarQubeEnv('sq1') {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }

  stage('SonarQube quality gate') {
    def qualityGateStatus = sh(returnStdout: true, script: "curl -s -X POST http://localhost:9000/api/qualitygates/project_status/your_project_key")
    if (qualityGateStatus.contains('ERROR')) {
      error('SonarQube quality gate failed')
    }
  }
}