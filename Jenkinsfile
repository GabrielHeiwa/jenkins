pipeline {
    agent any
    
    environment {
        BRANCH_NAME = "${env.GIT_BRANCH}"
    }
    
    stages {
        stage('Load Environment Variables') {
            steps {
                script {
                    // Split BRANCH_NAME by / and get branch name
                    def branchParts = BRANCH_NAME.split('/')
                    def branchName = branchParts[branchParts.length - 1]
                    echo "Branch name: ${branchName}"
                    // Load environment variables from the .env file
                    // The .env file should be named according to the branch name
                    def envFile = ".env.${BRANCH_NAME}"
                    if (fileExists(envFile)) {
                        def props = readFile(envFile).split('\n')
                        props.each { line ->
                            if (line && !line.startsWith('#')) {
                                def (key, value) = line.tokenize('=')
                                env[key] = value
                            }
                        }
                    } else {
                        echo "Environment file ${envFile} does not exist!"
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