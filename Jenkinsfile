podTemplate(inheritFrom: 'build', containers: [
    containerTemplate(name: 'build', image: 'maven:3.8.1-jdk-11')
]) {
    node(POD_LABEL) {
        stage('build') {
            echo 'Build code'
        }
        stage('test') {
            echo 'unit tests'
        }
        stage('deploy') {
            echo 'deploy to artifact repo'
        }
    }
}

