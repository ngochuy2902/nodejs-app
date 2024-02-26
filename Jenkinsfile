pipeline {
    agent {
        label 'master'
    }

    environment {
        NODE_VERSION = '18.18.2'
        DEPLOY_DIR = '/app/nodejs-app'
    }


    stages {
        stage('Build') {
            steps {
                echo 'Step 1: Building..'
                sh script: '''
                . ~/.nvm/nvm.sh
                nvm install $NODE_VERSION
                nvm use $NODE_VERSION
                node -v
                npm install
                '''.stripIndent()
                echo 'Build completed!'
            }
        }
        stage('Deploy') {
            steps {
                sh 'rm -rf /app/nodejs-app/*'
                sh 'cp -r * /app/nodejs-app'
                sh script: '''
                /var/lib/jenkins/.nvm/versions/node/v18.18.2/bin/pm2 start /app/nodejs-app/index.js
                '''.stripIndent()
                echo 'Deploy completed!'
            }
        }
    }
}
