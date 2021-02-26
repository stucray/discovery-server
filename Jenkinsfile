pipeline {
  agent any

  //Package the application without running tests.
  stages {
    stage("Package") {
            steps {
          echo 'Building and packaging Maven artifact.'
          sh 'mvn clean package -DskipTests=true'
      }
    }

    //Run unit tests.
    stage("Unit Tests") {
        steps {
            echo 'Running tests'
            sh 'mvn test'
        }
    }

    //Deploy artifact to maven repository
    stage("Deploy Maven Artifact") {
        steps {
            echo 'Deploying to Maven repository'
            sh 'mvn deploy -DskipTests=true'
        }
    }


    
    //Build Docker image
    stage("Build Docker Image") {
    
        steps {
            echo 'Building Docker image'
            sh 'mvn spring-boot:build-image -DskipTests=true'
        }
    }

  }

  post {
    always {
      cleanWs()
    }
  }
}
