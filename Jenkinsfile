node(){
	environment {
    MAVEN_HOME = tool 'Maven'
    JAVA_HOME = tool 'JDK 21'
}
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'bfa38064-13a6-4cd8-9b15-afa325457114', url: 'git@github.com:vrusalovskaya/jenkinsTest.git']])
	}
	stage('Build Automation'){
		sh """
			ls -lart

		"""
		sh "${MAVEN_HOME}/bin/mvn clean package"
		sh """
			ls -lart target

		"""
	}
	
	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: '8b3caa11-ac73-4d6b-b1e6-8183fc456db8', path: '', url: 'http://192.168.100.12:8080/')], contextPath: 'testApp', onFailure: false, war: 'target/*.war'
	}
}
