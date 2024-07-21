pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('nvd_api_key')
    }
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
                dependencyCheck additionalArguments: '--format HTML --format XML --suppression suppression.xml', odcInstallation: 'OWASP Dependency-Check Vulnerabilities', suppressionFile: '', apiUrl: 'https://services.nvd.nist.gov/rest/json/cves/1.0', apiKey: "${env.NVD_API_KEY}"
            }
        }
    }   
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}