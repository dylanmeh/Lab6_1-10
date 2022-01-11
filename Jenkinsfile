@Library("lab3") _ 
properties([pipelineTriggers([eventTrigger(jmespathQuery("unitTestEnable=='true' || unitTestEnable=='false'"))])])
podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.8.1-jdk-11', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('first conditional stage') {
            container('maven') {
                stage('enable unit testing when event is prod') {
                    String conditionalfunction() {
                    if (getTriggerCauseEvent.getTriggerCauseEvent() == 'true')
                        println 'enabling unit testing'    
                }
            }    
        }        
        stage('second conditional stage') {
            container('maven') {
                stage('disable unit testing when event is dev') {
                    if (getTriggerCauseEvent.getTriggerCauseEvent() == 'false')
                        println 'user disabled unit testing'
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