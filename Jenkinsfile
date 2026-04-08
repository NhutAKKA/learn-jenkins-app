pipeline {
    agent any

    environment {
        HTTP_PROXY = "${JENKINS_HTTP_PROXY_URL}"
        HTTPS_PROXY = "${JENKINS_HTTPS_PROXY_URL}"
        NO_PROXY = "${JENKINS_NO_PROXY}"
        http_proxy = "${JENKINS_HTTP_PROXY_URL}"
        https_proxy = "${JENKINS_HTTPS_PROXY_URL}"
        no_proxy = "${JENKINS_NO_PROXY}"
        npm_config_proxy = "${JENKINS_HTTP_PROXY_URL}"
        npm_config_https_proxy = "${JENKINS_HTTPS_PROXY_URL}"
        npm_config_registry = "https://registry.npmjs.org/"
    }

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                    args """
                        -e HTTP_PROXY=${JENKINS_HTTP_PROXY_URL}
                        -e HTTPS_PROXY=${JENKINS_HTTPS_PROXY_URL}
                        -e NO_PROXY=${JENKINS_NO_PROXY}
                        -e http_proxy=${JENKINS_HTTP_PROXY_URL}
                        -e https_proxy=${JENKINS_HTTPS_PROXY_URL}
                        -e no_proxy=${JENKINS_NO_PROXY}
                        -e npm_config_proxy=${JENKINS_HTTP_PROXY_URL}
                        -e npm_config_https_proxy=${JENKINS_HTTPS_PROXY_URL}
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
