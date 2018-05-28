node{
    stage('SCM'){
		git 'https://github.com/sunnydevops/game-of-life.git'
    }
    stage('Build'){
		withSonarQubeEnv('sonar'){
          sh 'mvn clean package sonar:sonar'
    }
	}
	stage("Quality Gate"){
		timeout(time: 1, unit: 'HOURS'){
			def qg = waitForQualityGate()
			if (qg.status != 'OK'){
				error "pipeline aborted due to quality gate failure: ${qg.status}"
			}
		}
	}
    stage('artifactory'){
        archive 'gameoflife-web/target/gameoflife.war'
        
    }
    stage('result'){
        junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
    
}