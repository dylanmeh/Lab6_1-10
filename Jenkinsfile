podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.8.1-jdk-11', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('build') {
            container('maven') {
                stage('build') {
                    echo 'Build code'
                }
            }    
        }        
        stage('test') {
            container('maven') {
                stage('test') {
                     echo 'unit tests'
                }
            }    
        }    
        stage('deploy') {
            container('maven') {
                stage('deploy') {
                    echo 'deploy to artifact repo'

                }
            }
        }        
    }
}

