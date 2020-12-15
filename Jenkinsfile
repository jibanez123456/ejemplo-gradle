pipeline {
    agent any

    stages {
        stage('Pipeline') {
            steps {
                script {
				
					stage('Build and Test') {
						// sh ".gladlew clean build"
						bat "gradlew clean build"
					}
					stage('Sonar') {
						// configurado en sonarcube-configuration
						def scannerHome = tool 'sonar-scanner';
						
						// conf generales
						withSonarQubeEnv('sonar-server') { 
							//sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build"
							bat "${scannerHome}\\bin\\sonar-scanner -Dsonar.projectKey=ejemplo-gradle -Dsonar.java.binaries=build"
						}
					}
					stage('Run') {
						//
					}
					stage('Test') {
						//
					}
					stage('Nexus') {
						//
					}
				}
            }
        }
    }
}

