properties([pipelineTriggers([eventTrigger(jmespathQuery("environment=='prod'"))])])
podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.8.1-jdk-11', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('first conditional stage') {
            container('maven') {
                stage('enable unit testing when event is prod') {
                    if (getTriggerCauseEvent.getTriggerCauseEvent() == 'prod')
                    echo 'enabling unit testing'
                    }
                    return "N/A" 
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