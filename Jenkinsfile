pipeline {
  agent {
    kubernetes {
      defaultContainer 'ubuntu'
      activeDeadlineSeconds 3600
      idleMinutes 15
    }
  }
  stages {
    stage('Init') {
      steps {
        checkout scm
	script {
	  def m = (env.GIT_URL =~ /(\/|:)(([^\/]+)\/)?(([^\/]+?)(\.git)?)$/)
	  if (m) {
	    org = m.group(3)
	    repo = m.group(5)
	  }
	}
      }
    }
    stage('Setup build') {
      when { not { buildingTag() } }
      steps {
        script {
          target = "verify"
        }
      }
    }
    stage('Setup release') {
      when { buildingTag(); not { changeRequest() }  }
      steps {
        script {
          target = "deploy -P release --settings settings.xml"
        }
        sh 'gpg --batch --import ism.key'
      }
    }
    stage('Build') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'jenkins-dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD'),
            usernamePassword(credentialsId: 'jenkins-ossrh', usernameVariable: 'OSSRH_USER', passwordVariable: 'OSSRH_PASS'),
            string(credentialsId: 'jenkins-gpg', variable: 'GPG_PASS')]) {
          withMaven {
            sh "./jdk-wrapper.sh ./mvnw $target -U -B -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=warn -Ddocker.verbose=true"
          }
        }
      }
    }
  }
  post('Analysis') {
    always {
      recordIssues(
          enabledForFailure: true, aggregatingResults: true,
          tools: [java(), checkStyle(reportEncoding: 'UTF-8'), spotBugs()])
    }
  }
}
