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
                    def records = readCSV file: 'input.csv'
                    assert records[0][0] == 'PreviousRunDate'
                    assert records[1][1] == 'b'        
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
