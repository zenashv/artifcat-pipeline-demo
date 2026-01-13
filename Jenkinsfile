pipeline{
  agent any

  stages{
    
    stage('Checkout') {
      steps {
        echo 'Fetching source code'
        checkout scm
      }
    }

    stage('Quality Check') {
      steps {
        echo 'Checking Code Quality'
        bat '''
        findstr GOOD quality.txt > nul
        if errorlevel 1 (
              echo Code Quality Failed
              exit 1
        ) else (
              echo Code Quality Pass
        ) 
        '''
        
      }
    }
    stage('Generate Report') {
      steps {
        echo 'Generating build report'
        bat '''
        mkdir report
        echo Build Successful > reports\\build-report.txt
        '''
        
      }
    }

    stage ('Archive Artifacts') {
      steps {
        echo 'Archiving reports'
        archiveArtifacts artifacts: 'reports/*.txt', fingerprint: true
      }
  }
  }
    post {
      success {
        echo 'Pipeline completed successfully'
      }
      failure {
        echo 'Pipeline failed- code blocked'
    }
  }
}
