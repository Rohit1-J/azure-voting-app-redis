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
                    /usr/local/bin/docker build -t rohit1/jenkins-pipeline .
                    /usr/local/bin/docker images -a
                    cd ..
                    env
                """)
            }
        }
        stage('Docker push') {
            steps {
                echo "Workspace is $WORKSPACE"
                dir("$WORKSPACE/azure-vote"){
                    script{
                        
                        // docker.withRegistry("https://index.docker.io/v1", 'Dockerhub'){
                            def image = docker.build('rohit1/jenkins-pipeline:latest')
                            image.push()
                        // }
                    }
                }
            }
        }
    }
}
