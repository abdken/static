pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Lint HTML') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }

        
        stage('Upload to AWS') {
            steps {
                withAWS(region:'ca-central-1',credentials:'a3654d1a-37fa-468a-8157-cb7165d12d50') {
                sh 'echo "Uploading content with AWS creds"'
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-devops-pipeline')
                }
            }
        }
    }
}
