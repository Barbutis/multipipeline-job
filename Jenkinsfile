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
                    println("Branch One")
                }
            }
        }
        
        stage ('Application and Tests inside container'){
            steps {
                script {
                    env.FINISHED_STAGE = env.STAGE_NAME
                    docker.image('mysql:5').withRun('-e "MYSQL_ROOT_PASSWORD=my-secret-pw"') { c ->
                        docker.image('mysql:5').inside("--link ${c.id}:db") {
                            /* Wait until mysql service is up */
                            sh 'while ! mysqladmin ping -hdb --silent; do sleep 1; done'
                            sh 'echo "all ok"'
                        }
                    }
                }
            }
        }
    }
}
