podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3/8/1-jdk-11', command 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('build') {
            container('maven')
            echo 'Build code'
        }
        stage('test') {
            container('maven')
            echo 'unit tests'
        }
        stage('deploy') {
            container('maven')
            echo 'deploy to artifact repo'
        }
    }
}

