
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

        stage('--verify settings.xml--') {
            steps {
                sh '''
                    test -s /var/lib/jenkins/.m2/settings.xml
                    echo "Nexus settings.xml found"
                '''
            }
        }

        stage('--deploy to Nexus--') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('--verify WAR file--') {
            steps {
                sh '''
                    ls -lh target/stud-reg-war-0.0.1-SNAPSHOT.war
                '''
            }
        }

        stage('--deploy to Tomcat--') {
            steps {
                sh '''
                    cp target/stud-reg-war-0.0.1-SNAPSHOT.war \
                    /var/lib/tomcat10/webapps/student-app.war
                '''
            }
        }
    }
}

