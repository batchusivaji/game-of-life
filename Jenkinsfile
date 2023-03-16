pipeline {
    agent { label 'JDK_NODE' }
    triggers { 
        pollSCM ('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/batchusivaji/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8'
            }
            steps {
                sh 'mvn package'
            }
        }
        stage( 'artifacts' ) {
            steps {
                archiveArtifacts artifacts: '**/target/*.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }     
    }
}    
 