pipeline {
    agent { label 'JDK_8' }
    triggers { 
        pollSCM ('* * * * *') 
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/batchusivaji/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage( 'post build' ) {
            steps {
                archiveArtifacts artifacts: '**/target/*.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }     
    }
}    