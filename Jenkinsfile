pipeline {
 agent any

 stages {
   stage('build') {
     steps {
      sh 'ant -f build.xml -v'
      sh 'echo "GITHUB HOOK SUCCESS"'
     }
   }
 }
}
