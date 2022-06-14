pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                script {
                   def date = new Date()
                   def now = date.format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                   env.CURRENT_RUN_TIMESTAMP=now
                   echo 'Current  .. ' +now       
                  
                    build = currentBuild
                    while(build != null && build.result != 'SUCCESS') {
                        build = build.previousBuild
                    }
                    
                    echo 'Previous build result: ' + build.result
                    echo 'Prevoius LAST_RUN_TIMESTAMP: ' + build.buildVariables.CURRENT_RUN_TIMESTAMP
                    
                    if (build.buildVariables.CURRENT_RUN_TIMESTAMP != null) {
                        env.LAST_RUN_TIMESTAMP=build.buildVariables.CURRENT_RUN_TIMESTAMP
                    } else {
                         env.LAST_RUN_TIMESTAMP=now.plus(-1)
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
