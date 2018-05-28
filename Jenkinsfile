node{
    stage('SCM'){
      git 'https://github.com/wakaleo/game-of-life.git'
    }
    stage('Build'){
        sh 'mvn package'
    }
    stage('artifactory'){
        archive 'gameoflife-web/target/gameoflife.war'
        
    }
    stage('result'){
        junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
    
}