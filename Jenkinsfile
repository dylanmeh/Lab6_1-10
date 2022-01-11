@Library("lab3") _ 
properties([pipelineTriggers([eventTrigger(jmespathQuery("unitTestEnable=='true' || unitTestEnable=='false'"))])])
podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.8.1-jdk-11', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('SCM Checkout') {
            git url: 'https://github.com/dylanmeh/Lab6_1-10.git', branch: 'main'

        }
        stage('first conditional stage') {
            container('maven') {
                stage('enable unit testing when event is prod') {
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
        stage('buildstart') {
            container('maven') {
                stage('buildStart Time Stage') {
                    buildStart()
                }
            }
        }
        stage('build') {
            container('maven') {
                stage('build') {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }        
        stage('test') {
            container('maven') {
                stage('test') {
                    sh 'mvn test'
                }
                post {
                    always {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        }
        stage('deploy') {
            container('maven') {
                stage('deploy') {
                    sh './scripts/deliver.sh'
                }           
            }
        }
        post {
            success {
                buildResultsEmail("Successful")
            }
            failure {
                buildResultsEmail("Failure")
            }
        }
    }
}