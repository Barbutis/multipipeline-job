pipeline {
    agent any

    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '30'))
    }
    
    stages {
      stage('Begin'){
            steps {
                script{
                    println("Main Branch")
                }
            }
        }
    }
}
