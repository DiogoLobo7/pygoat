pipeline {
   environment {
      QODANA_TOKEN=credentials('qodana-token')
   }
   agent {
      docker {
         args '''
         -v "${WORKSPACE}":/data/project
         --entrypoint=""
         '''
         image 'jetbrains/qodana-js'
      }
   }
   stages {
      stage('Qodana') {
         steps {
            sh '''qodana'''
         }
      }
   }
}
