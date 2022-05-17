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
                    //def lastSuccessBuildName = Jenkins.instance.getItem(env.JOB_NAME).lastSuccessfulBuild.displayName
                    echo "Last Success Build Name: "currentBuild.previousSuccessfulBuild
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
