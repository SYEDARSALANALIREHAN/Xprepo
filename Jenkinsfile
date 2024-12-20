pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    sh '''
                        ls
                        npm install
                        echo "Turning analytics off"
                        ng build --prod
                        ls dist
                        cd dist && ls
                        cd dist/angular-tour-of-heroes/browser && ls
                    '''
                }
            }
        }

        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '904061d4-f61d-4f1a-96f0-7dc23b25e9a0') {
                    sh '''
                        ls -la
                        aws s3 cp dist/angular-tour-of-heroes/browser/ s3://xprepo-bucket/ --recursive
                    '''
                }
            }
        }
    }
}
