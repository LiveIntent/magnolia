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
							echo $SBT_CREDENTIALS
							sbt coreJVM/test
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