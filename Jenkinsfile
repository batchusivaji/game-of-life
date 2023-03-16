pipeline {
    agent any
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
        stage ('package') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"'
                sh 'mvn package'
            }
        }
        stage ( 'post build' ) {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }     
    }
}    