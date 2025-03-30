pipeline {
    agent any
    
    stages {
        stage('Load Environment Variables') {
            steps {
                script {
                    // Get branch name by env GIT_BRANCH split by '/'
                    def branchName = env.GIT_BRANCH.split('/').last()
                    // Define the path to the environment file
                    def MY_ENV_FILE = ".env.${branchName}"
                    // Check if the file exists
                    if (!fileExists(MY_ENV_FILE)) {
                        error "Environment file ${MY_ENV_FILE} does not exist."
                    }
                    def envVars = readFile("${MY_ENV_FILE}").split("\n").findAll { it && !it.startsWith("#") }
                    def envList = envVars.collect { line ->
                        def (key, value) = line.tokenize('=')
                        "${key.trim()}=${value.trim()}"
                    }
                    withEnv(envList) {
                        sh 'echo $MY_VARIABLE'
                        sh 'env | sort'
                    }
                }
            }
        }

        stage('Print Environment Variables') {
            steps {
                script {
                    echo "Loaded environment variables:"
                    sh 'env | sort'
                }
            }
        }
    }
}
