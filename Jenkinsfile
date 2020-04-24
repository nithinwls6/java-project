pipeline {
 agent any
 options{
   buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
 }
 stages {
   stage('build') {
     steps {
      sh 'ant -f build.xml -v'
      sh 'echo "GITHUB HOOK SUCCESS"'
     }
   }
   stage('UnitTest'){
     sh 'ant -f test.xml -v'
     junit 'reports/result.xml'
   }
 }

 post {
   always{
     archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
   }
 }
}
