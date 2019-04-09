// start - Auxiliary functions
def node_details() {
    sh """
    printf "Node          : ${env.NODE_NAME}\nHostname      : \$(hostname)\n\$(docker --version)\n"
    """
}

def open_pr(){
  
}

// end - Auxiliary fuctions

pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
    }
    environment{
        project_name='node_sample'
    }
    stages {
        stage('init') {
            steps {
                script {
                    node_details()
                }
            }
        }
        stage('Artifacts Test'){
            steps{
               sh "cat package.json"
               open_pr() 
            }
        }
    }
    post {
        always {
            deleteDir()
        }
        unstable {
              echo "UNSTABLE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
        }
        failure {
              echo "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})"
        }
    }
}
