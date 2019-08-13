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
							sbt '+ coreJVM/publish'
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