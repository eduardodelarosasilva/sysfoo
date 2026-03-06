pipeline {
    agent any // 
    tools {
      maven 'Maven 3.9.12'
    }
    stages {
        stage("build") {
            steps {
                echo 'Compiling sysfoo' // 
                sh 'mvn compile'
            }
        }
        stage("test") {
            steps {
                echo 'Running unit test ' // 
                sh 'mvn clean test'
            }
        }
        stage("package") {
            steps {
                echo 'Packing the app' // 
                sh 'mvn package -DskipTest'
            }
        }
    }
    
    post {
        always {
            echo 'This pipeline is completed..' // 
        }
    }
}
