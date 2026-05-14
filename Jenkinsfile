def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]

pipeline {
    agent any

    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }

    environment {

        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'

        NEXUSIP = '172.31.19.169'
        NEXUSPORT = '8081'

        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'

        SONARSERVER = 'sonarserver'
        SONARSCANNER = 'sonarscanner'

    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn -s settings.xml clean install -DskipTests'
            }

            post {
                success {
                    echo "Archiving WAR artifact..."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }

        stage('Sonar Analysis') {

            environment {
                scannerHome = tool "${SONARSCANNER}"
            }

            steps {

                withSonarQubeEnv("${SONARSERVER}") {

                    sh """
                    ${scannerHome}/bin/sonar-scanner \
                    -Dsonar.projectKey=vprofile \
                    -Dsonar.projectName=vprofile \
                    -Dsonar.projectVersion=${BUILD_NUMBER} \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/classes \
                    -Dsonar.junit.reportsPath=target/surefire-reports/ \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {

        always {

            echo 'Sending Slack notification...'

            slackSend(
                channel: '#jenkinscicd',
                color: COLOR_MAP[currentBuild.currentResult],

                message: """
*${currentBuild.currentResult}:* Job ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }
    }
}