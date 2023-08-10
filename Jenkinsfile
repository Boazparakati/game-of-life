pipeline {
    agent {label 'JDK-8'}
    option {
        timeout(time: 10, unit: 'MINUTES')
    }
    triggers {
        pollSCM('* * * * *')
    }
    tools {
        maven 'Mvn_3.6'
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/Boazparakati/game-of-life.git',
                branch: 'master'
            }
        }
        stage('build and package') {
            steps {
                sh 'mvn package'
            } 
        }
        stage('reporting') {
            steps {
                archiveArtifacts artifacts: '**/gameoflife.war'
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}