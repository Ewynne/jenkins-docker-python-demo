node {
    stage('Checkout SCM') {
        checkout scm
    }
    withEnv(["PATH+DOCKER=${tool 'docker'}"]) {
        def pythonImage
        stage('build docker image') {
            pythonImage = docker.build("maxsum:build")
        }
        stage('test') {
            pythonImage.inside {
                sh '. /tmp/venv/bin/activate && python -m pytest --junitxml=build/results.xml'
            }
        }
        stage('collect test results') {
            junit 'build/results.xml'
        }
    }
}
