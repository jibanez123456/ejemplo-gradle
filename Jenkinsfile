pipeline {
    agent any

	parameters { choice(name: 'tool', choices: ['gradle', 'maven'], description: 'Selección herramienta de Construcción') }
    
    stages {
        stage('Pipeline') {
            steps {
                script {
				
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
}
