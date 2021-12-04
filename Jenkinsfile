pipeline{
    agent{ label 'express'}
    triggers{
        pollSCM('H * * * *')
    }
    parameters{
        string(name: 'BRANCH', defaulValue: 'master', discription: 'branch to build')
    }
    stages{
        stage{
            steps('scm'){
                 git branch: "${paramsBRANCH}", url:'https://github.com/greddy26/game-of-life-1.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn package'
                stash name: 'game-of-life.war' , include: '**/*.war'
            }
        }
    }
    post{
        success{
            junit '**/TEST-*.xml'
            archive '**/*.war'

        }
    }
}