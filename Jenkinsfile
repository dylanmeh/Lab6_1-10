podTemplate(yaml: '''
    apiVersion: v1
    kind: Pod
    spec:
        containers:
        - name: build
        image: maven:3.8.1-jdk-11
        command:
        - cat
        args:
        - 99d
''') {
    node('POD_LABEL') {
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

