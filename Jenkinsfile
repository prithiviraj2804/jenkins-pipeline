pipeline {
    agent any
    
    tools {
        maven '3.9.4'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '172.19.0.1', description: 'Remote Staging Server')
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                        sh "echo binary@01 | sudo -S cp -r **/*.war /opt/tomcat/latest/webapps"
                    }
                }
            }
        }
    }
}
