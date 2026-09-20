pipeline {
    agent any

    parameters {
        choice(name: 'ENVIRONMENT', choices: ['dev', 'uat', 'prod'], description: 'Select deployment environment')
    }

    environment {
        APP_NAME    = 'vel-app'
        DEPLOY_PATH = "/var/www/${APP_NAME}/${params.ENVIRONMENT}"
        GIT_URL     = 'https://github.com/pkmore2018/vel-app.git'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                git branch: 'master', url: "${GIT_URL}"
            }
        }

        stage('Validate HTML') {
            steps {
                sh 'ls -lrht'
                sh '''
                    for f in *.html; do
                        echo "Checking $f"
                        grep -qi "<html" "$f" || { echo "$f is not valid HTML"; exit 1; }
                    done
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENVIRONMENT} at ${DEPLOY_PATH}"
                sh """
                    sudo mkdir -p ${DEPLOY_PATH}
                    sudo rm -rf ${DEPLOY_PATH}/*

                    if [ "${params.ENVIRONMENT}" = "dev" ]; then
                        sudo cp dev.html ${DEPLOY_PATH}/index.html
                    elif [ "${params.ENVIRONMENT}" = "uat" ]; then
                        sudo cp uat.html ${DEPLOY_PATH}/index.html
                    else
                        sudo cp index.html ${DEPLOY_PATH}/index.html
                    fi

                    sudo chown -R www-data:www-data ${DEPLOY_PATH}
                    sudo chmod -R 755 ${DEPLOY_PATH}
                """
            }
        }

        stage('Verify') {
            steps {
                sh """
                    echo "Files deployed to ${DEPLOY_PATH}:"
                    ls -lrht ${DEPLOY_PATH}
                """
            }
        }
    }

    post {
        success { echo "✅ Deployment to ${params.ENVIRONMENT} succeeded!" }
        failure { echo "❌ Deployment failed. Check logs above." }
    }
}
