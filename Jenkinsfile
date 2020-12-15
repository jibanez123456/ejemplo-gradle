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
						bat "gradle bootRun &"
						sleep 20
					}
					stage('Test') {
						//
						sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'

					}
					stage('Nexus') {
						//
						steps {
						   nexusPublisher nexusInstanceId: 'nexus', 
						   nexusRepositoryId: 'test-repo',
						   packages: [
							   [$class: 'MavenPackage', mavenAssetList: [
								   [
									   classifier: '', 
									   extension: 'jar', 
									   filePath: 'C:\\Users\\jibanez\\.jenkins\\workspace\\emplo-gradle_feature-dir-inicial\\DevOpsUsach2020-0.0.1.jar'
									]
								], 
								mavenCoordinate: [
									artifactId: 'DevOpsUsach2020', 
									groupId: 'com.devopsusach2020', 
									packaging: 'jar', 
									version: '1.0.0'
								]
							]
						]
						}
					}
				}
            }
        }
    }
}