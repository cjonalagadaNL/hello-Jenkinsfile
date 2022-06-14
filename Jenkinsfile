pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                script {
                   def date = new Date()
                   def now = date.format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                   env.BUILDVERSION=now
                   def last = readFile(file: 'SalesReportLastRun.txt')
                   echo 'Last  .. ' +last
                   writeFile(file: 'SalesReportLastRun.txt', text: now)
                   echo 'Current  .. ' +now       
                  
                    def changes = "Changes:\n"
                    build = currentBuild
                    while(build != null && build.result != 'SUCCESS') {
                        
                        changes += "In ${build.id}:\n"
                        for (changeLog in build.changeSets) {
                            for(entry in changeLog.items) {
                                for(file in entry.affectedFiles) {
                                    changes += "* ${file.path}\n"
                                }
                            }
                        }
                        build = build.previousBuild
                    }
                    echo changes
                   
                    echo 'Previous build result: ' + currentBuild.getPreviousBuild().result
                    echo 'Prevoius build description: ' +currentBuild.previousBuild.description
                    echo 'Prevoius build id: ' +currentBuild.previousBuild.getId()
                    echo 'Prevoius BUILDVERSION: ' + currentBuild.previousBuild.buildVariables.BUILDVERSION
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
