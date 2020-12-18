pipeline {
    agent any

	parameters { choice(name: 'tool', choices: ['gradle', 'maven'], description: 'Selección herramienta de Construcción') }
    
    stages {
        stage('Pipeline') {
            steps {
                script {

                	env.TAREA = ''
				
					params.tool

					if (params.tool == 'gradle') { 
							def ejecucion = load 'gradle.groovy'
							ejecucion.call()
					}
					else {
							def ejecucion = load 'maven.groovy'
							ejecucion.call()
					}
				}
            }
        }
    }	

    // slackSend message: '[José Ibañez] [NOMBRE_DE_JOB] [BUILD_TOOL] [Ejecución exitosa] ', teamDomain: 'devops-usach-2020', tokenCredentialId: 'slacktoken'

    post {

    	success {
    		 slackSend message: '[Jose Ibañez] [' + env.JOB_NAME + '] [' + params.tool  + '] [Ejecucion exitosa] ', teamDomain: 'devops-usach-2020', tokenCredentialId: 'slacktoken'
    	}

    	failure {
    		 slackSend message: '[Jose Ibañez] [' + env.JOB_NAME + '] [' + params.tool  + '] [Ejecucion fallida en stage:' + env.TAREA + '] ', teamDomain: 'devops-usach-2020', tokenCredentialId: 'slacktoken'
    	}
    }
}
