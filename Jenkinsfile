#!groovy

properties([
	[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10']],
	disableConcurrentBuilds()
]);

def PRODUCT = 'magnolia'
def WORKSPACE = "workspace/${PRODUCT}"

try {
	node('sbt') {
		ws(WORKSPACE) {
			checkout scm
			
			container('sbt') {
			    stage('Build') {
			        ansiColor('xterm') {
						sh """
							ls /tmp/secrets/build.idtargeting.com.credentials/
						
							sbt +compile +tests/run
			            """
			        }
				}
			}
		}
	}
} catch (exception) {
	throw exception
} finally {
}