pipeline {
 agent 'master'
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
     steps{
     sh 'ant -f test.xml -v'
     junit 'reports/result.xml'
     }
   }
 }
 stage('Deploy'){
   steps{
     sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectanles/all/"
   }
 }

 post {
   always{
     archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
   }
 }
}
