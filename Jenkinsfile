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
       sh "trivy fs ."
 }
  stage('docker build & push'){
   sh 'docker build --build-arg TMDB_V3_API_KEY=6186ad8a917f08f30805e6a364e37a85 -t netflix .'
   sh 'docker tag netflix devopswthaws58/netflix:latest'
   sh 'docker login -u ${{secrets.DOCKERHUB_USERNAME}} -p ${{secrets.DOCKERHUB_TOKEN}}'
   sh 'docker push devopswthaws58/netflix:latest'
  }
}
