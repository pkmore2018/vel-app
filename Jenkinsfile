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
}stage('Deploy') {
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
