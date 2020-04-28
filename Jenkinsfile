pipeline {
 agent none

 options{
   buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '1'))
 }
 stages {
   stage('build') {
     agent {
       label 'apache'
     }
     steps {
      sh 'ant -f build.xml -v'
      sh 'echo "GITHUB HOOK SUCCESS"'
     }
     post {
       always{
         archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
       }
     }
   }
   stage('UnitTest'){
     agent {
       label 'apache'
     }
     steps{

     sh 'ant -f test.xml -v'
     junit 'reports/result.xml'
     }
   }

 stage('Deploy'){
   agent {
     label 'apache'
   }
   steps{
     sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
   }
 }
 stage("Running on CentOS") {
   agent {
     label 'Dev'
   }
   steps {
     sh "wget http://10.3.26.21/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
     sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 4 5"
   }
 }
 stage("Running on Debiann") {
   agent {
     docker 'openjdk:8u121-jre'
   }
   steps{
     sh "wget http://10.3.26.21/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
     sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 8 10"
   }
 }
}

}
