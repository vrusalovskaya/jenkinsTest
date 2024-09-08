node(){
	environment {
        MAVEN_HOME = tool name: 'Maven', type: 'maven'
        JAVA_HOME = tool name: 'JDK 21', type: 'jdk'
        PATH = "${MAVEN_HOME}/bin:${PATH}"            
    }
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'bfa38064-13a6-4cd8-9b15-afa325457114', url: 'git@github.com:vrusalovskaya/jenkinsTest.git']])
	}
	stage('Build Automation'){
		sh """
			ls -lart

		"""
		sh "/opt/apache-maven-3.9.9/bin/mvn clean package"
		sh """
			ls -lart target

		"""
		sh """
			ls -lart

		"""
	}
	
	stage('Code Deployment'){
		 steps {
                script {
                    def response = httpRequest acceptType: 'APPLICATION_JSON',
                                              url: 'http://192.168.100.12:8080/manager/text/deploy?path=/test123',
                                              authentication: '8b3caa11-ac73-4d6b-b1e6-8183fc456db8',
                                              requestBody: sh(script: "cat target/jenkinstest-0.0.1-SNAPSHOT.jar", returnStdout: true)
                    echo "Response: ${response}"
                }
            }
	}
}
