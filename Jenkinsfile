
pipeline {
    agent any

    stages {
        stage('--clean--') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('--compile--') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('--test--') {
            steps {
                sh 'mvn test'
            }
        }

        stage('--package--') {
            steps {
                sh 'mvn package'
            }
        }

        stage('--install--') {
            steps {
                sh 'mvn install'
            }
        }

        stage('--deploy to Nexus--') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'nexus-credentials',
                        usernameVariable: 'NEXUS_USERNAME',
                        passwordVariable: 'NEXUS_PASSWORD'
                    )
                ]) {
                    sh 'mvn -s /var/lib/jenkins/.m2/settings.xml deploy'
                }
            }
        }

        stage('--deploy to Tomcat--') {
            steps {
                sh '''
                    sudo cp target/*.war \
                    /var/lib/tomcat10/webapps/student-app.war
                '''
            }
        }
    }
}

