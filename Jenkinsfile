pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                script {
                   def today = new Date()
                   def yesterday = today - 1
                   env.CURRENT_RUN_TIMESTAMP=today.format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                   build = currentBuild
                   while(build != null && build.result != 'SUCCESS') {
                        build = build.previousBuild
                    }
                    
                    echo 'Previous build result: ' + build.result
                    echo 'Prevoius LAST_RUN_TIMESTAMP: ' + build.buildVariables.CURRENT_RUN_TIMESTAMP
                    
                    if (build.buildVariables.CURRENT_RUN_TIMESTAMP != null) {
                         env.LAST_RUN_TIMESTAMP=yesterday.format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                       
                    } else {
                         env.LAST_RUN_TIMESTAMP=build.buildVariables.CURRENT_RUN_TIMESTAMP
                    }
                    
                     echo ' env.LAST_RUN_TIMESTAMP: ' + env.LAST_RUN_TIMESTAMP
              }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'SalesReportLastRun.txt', onlyIfSuccessful: true
        }
    }
}
