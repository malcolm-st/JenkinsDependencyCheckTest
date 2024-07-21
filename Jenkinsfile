pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			 steps {
                script {
                    git branch: "master",
                        url: "https://github.com/malcolm-st/JenkinsDependencyCheckTest.git"
                }
            }
		}

		stage('OWASP DependencyCheck') {
			steps {
				 dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}