pipeline {
    agent any

    environment {
        HTTP_PROXY = "${env.JENKINS_HTTP_PROXY_URL}"
        HTTPS_PROXY = "${env.JENKINS_HTTPS_PROXY_URL}"
        NO_PROXY = "${env.JENKINS_NO_PROXY}"
        http_proxy = "${env.JENKINS_HTTP_PROXY_URL}"
        https_proxy = "${env.JENKINS_HTTPS_PROXY_URL}"
        no_proxy = "${env.JENKINS_NO_PROXY}"
        npm_config_proxy = "${env.JENKINS_HTTP_PROXY_URL}"
        npm_config_https_proxy = "${env.JENKINS_HTTPS_PROXY_URL}"
        npm_config_registry = "https://registry.npmjs.org/"
    }

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                    args """
                        -e HTTP_PROXY=${env.JENKINS_HTTP_PROXY_URL}
                        -e HTTPS_PROXY=${env.JENKINS_HTTPS_PROXY_URL}
                        -e NO_PROXY=${env.JENKINS_NO_PROXY}
                        -e http_proxy=${env.JENKINS_HTTP_PROXY_URL}
                        -e https_proxy=${env.JENKINS_HTTPS_PROXY_URL}
                        -e no_proxy=${env.JENKINS_NO_PROXY}
                        -e npm_config_proxy=${env.JENKINS_HTTP_PROXY_URL}
                        -e npm_config_https_proxy=${env.JENKINS_HTTPS_PROXY_URL}
                        -e npm_config_registry=https://registry.npmjs.org/
                    """
                }
            }
            steps {
                // ensure git is available inside the docker agent and perform a full clone
                sh 'apk add --no-cache git'
                sh '''
                    # remove any leftover .git then clone fresh into workspace
                    rm -rf .git || true
                    git clone --depth=1 https://github.com/NhutAKKA/learn-jenkins-app.git .
                '''
                sh'''
                    npm ci
                    npm run build
                '''
            }
        }
    }
}
