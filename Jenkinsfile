pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                sh "docker pull maven:3-alpine"
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -t='ashuch/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'Docker90*#', usernameVariable: 'ashuchaudhary')]) {
			        sh "docker login --username='ashuchaudhary' --password='Docker90*#'"
			        sh "docker tag ashuch/selenium-docker:ashuimagetag ashu_repo1:ashuimagetag"
			        sh "docker push ashu_repo1:ashuimagetag"
			    }
            }
        }
    }
}