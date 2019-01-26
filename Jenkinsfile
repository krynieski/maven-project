pipeline {
    agent any

    tools {
        maven 'localMaven'
    }

    parameters {
        string(name: 'tomcat_staging', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage ('Build') {
            steps {
                echo "Building..."
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Now Archiving..."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployment') {
            parallel {
                stage ('Deploy to Staging') {
                    steps {
                        sh "cp **/target/*.war \"/media/krynieski/Media/Dokumenty/Nauka/2018/CI Training/Jenkins & JAVA (Udemy course)/tools/apache-tomcat-8.5.37-staging/webapps\""
                    }
                }

                stage ('Deploy to Production') {
                    steps {
                        sh "cp **/target/*.war \"/media/krynieski/Media/Dokumenty/Nauka/2018/CI Training/Jenkins & JAVA (Udemy course)/tools/apache-tomcat-8.5.37-prod/webapps\""
                    }
                }
            }
        }
    }

}