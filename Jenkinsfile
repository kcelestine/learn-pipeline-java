pipeline {
  agent any
  
  stages {
    stage('one') {
      steps {
        echo 'first stage'
      }
    }
    stage('two') {
      steps {
        sh 'echo test > log.txt'
        
        archiveArtifacts artifacts: 'log.txt', followSymlinks: false
      }
    }
    stage('three') {
      steps {
        sh 'echo test > three.txt'
        
        archiveArtifacts artifacts: 'three.txt', followSymlinks: false
          // send to email
  emailext (
      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
      recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )

      }
    }
  }
}
