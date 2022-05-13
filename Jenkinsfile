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
                    def jsonString = '{"name":"katone","age":5}'
                    def jsonObj = readJSON text: jsonString

                    assert jsonObj['name'] == 'katone'  // this is a comparison.  It returns true
                    sh "echo ${jsonObj.name}"  // prints out katone
                    sh "echo ${jsonObj.age}"   // prints out 5
                    
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
