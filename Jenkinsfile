pipeline {
    agent any
    
    environment {
        BRANCH_NAME = "${env.BRANCH_NAME}"
    }
    
    stages {
        stage('Load Environment Variables') {
            steps {
                script {
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