pipeline {
    agent {
        docker {
            image 'node:14' // Use the desired Node.js version
            args '-u root' // Optional: Run Docker container as root
        }
    }
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        S3_BUCKET = 'p3l1devops'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Upload') {
            steps {
                sh 'npm install' // Install dependencies
                sh 'npm start' // Start your application (if applicable)
                sh 'npm run build' // Run custom npm script (if applicable)
                sh 'aws s3 cp /path/to/your/build/folder s3://$S3_BUCKET/ --recursive' // Upload build artifacts to S3
            }
        }
    }
}
