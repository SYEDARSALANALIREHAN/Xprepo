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
                withAWS(region: 'us-east-1', credentials: '984de098-9c5b-4d72-a3dc-6c6aa8744c00') {
                    sh '''
                        ls -la
                        aws s3 cp dist/angular-tour-of-heroes/browser/ s3://xprepo-bucket/ --recursive
                    '''
                }
            }
        }
    }
}
