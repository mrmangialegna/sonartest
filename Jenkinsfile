pipeline {
  agent any
  stages {
    stage('Analisi SonarQube') {
      steps {
        withSonarQubeEnv('sonarqube') {
          sh '''
            python3 -m venv .venv
            . .venv/bin/activate
            pip install pysonar
            pysonar --sonar-host-url=$SONAR_HOST_URL --sonar-token=$SONAR_AUTH_TOKEN
          '''
        }
      }
    }
    stage('Quality Gate') {
      steps {
        timeout(time: 5, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
