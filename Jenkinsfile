pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				git 'https://github.com/malcolm-st/JenkinsDependencyCheckTest'
			}
		}

		stage('OWASP DependencyCheck') {
			steps {
				 dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}