pipeline {
    agent any
    tools {
        maven "Maven"
    }
    stages {
        stage("Test"){
            steps{
                // mvn test
                sh "mvn test"
                //slackSend channel: 'testslack', message: 'Job Started' //to send email notification; add plugin in jenkins server as "slack notification" and install "jenkins" integrtion in slack.
            }
        }
        
        stage("Build"){
            steps{
                sh "mvn package"
            }
        }
        
        stage("Deploy on Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.20.20:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
        
        stage("Deploy on Prod"){
            input{
                message "Should we continue?"
                ok "Yes."
            }
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://192.168.20.21:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    
    post{
        always{
            echo "always"
        }
        success{
            echo "success"
            //slackSend channel: 'testslack', message: 'Success'
        }
        failure{
            echo "failure"
            //slackSend channel: 'testslack', message: 'Job Failed'
        }
    }
}
