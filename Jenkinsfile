pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh(script: '/usr/local/bin/docker images -a')
                sh(script: """
                    cd azure-vote
                    /usr/local/bin/docker build -t jenkins-pipeline .
                    /usr/local/bin/docker images -a
                """)
            }
        }
    }
}
