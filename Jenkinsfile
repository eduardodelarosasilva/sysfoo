pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Compiling sysfoo'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Running unit test '
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'Packing the app'
        sh '''# Truncar el ID del commit a 7 caracteres para un nombre limpio
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)

# Inyectar esa versión en el pom.xml de Maven antes de empaquetar
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
        sh 'mvn package -DskipTest'
        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'M3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}