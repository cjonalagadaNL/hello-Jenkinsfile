pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                script {
                   def date = new Date()
                   def now = date.format("yyyy-MM-dd HH:mm:ss.SSS", TimeZone.getTimeZone('UTC'))
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
                    echo 'Get Previous Build: ' + build.getPreviousBuild()
                    
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
}
