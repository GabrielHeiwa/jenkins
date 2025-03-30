pipeline {
    agent any
    environment {
        MY_ENV_FILE = ".env.master"
    }
    stages {
        stage('Load Environment Variables') {
            steps {
                script {
                    def envVars = readFile("${MY_ENV_FILE}").split("\n").findAll { it && !it.startsWith("#") }
                    def envList = envVars.collect { line ->
                        def (key, value) = line.tokenize('=')
                        "${key.trim()}=${value.trim()}"
                    }
                    withEnv(envList) {
                        sh 'echo $MY_VARIABLE'
                    }
                }
            }
        }
    }
}
