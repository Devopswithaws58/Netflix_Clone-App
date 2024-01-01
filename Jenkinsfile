node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar-scanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
 stage('Scan with Trivy') {
        steps {
            script {
               sh "trivy fs ."
            }
        }
   }
}
