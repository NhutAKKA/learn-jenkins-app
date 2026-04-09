pipeline {
    agent any

    environment {
        HTTP_PROXY = "${env.HTTP_PROXY ?: ''}"
        HTTPS_PROXY = "${env.HTTPS_PROXY ?: ''}"
        NO_PROXY = "${env.NO_PROXY ?: ''}"
        http_proxy = "${env.http_proxy ?: ''}"
        https_proxy = "${env.https_proxy ?: ''}"
        no_proxy = "${env.no_proxy ?: ''}"
        npm_config_proxy = "${env.HTTP_PROXY ?: ''}"
        npm_config_https_proxy = "${env.HTTPS_PROXY ?: ''}"
        npm_config_registry = "https://registry.npmjs.org/"
    }

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                    args """
                        -e HTTP_PROXY=${env.HTTP_PROXY ?: ''}
                        -e HTTPS_PROXY=${env.HTTPS_PROXY ?: ''}
                        -e NO_PROXY=${env.NO_PROXY ?: ''}
                        -e http_proxy=${env.http_proxy ?: ''}
                        -e https_proxy=${env.https_proxy ?: ''}
                        -e no_proxy=${env.no_proxy ?: ''}
                        -e npm_config_proxy=${env.HTTP_PROXY ?: ''}
                        -e npm_config_https_proxy=${env.HTTPS_PROXY ?: ''}
                        -e npm_config_registry=https://registry.npmjs.org/
                    """
                }
            }
            steps {
                sh'''
                    npm ci
                    npm run build
                '''
            }
        }
    }
}
