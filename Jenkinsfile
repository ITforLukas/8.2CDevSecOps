pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(
                    credentialsId: 'SONAR_TOKEN',
                    variable: 'SONAR_TOKEN'
                )]) {
                    sh '''
                        npx sonar-scanner \
                          -Dsonar.projectKey=ITforLukas_8.2CDevSecOps \
                          -Dsonar.organization=itforlukas \
                          -Dsonar.host.url=https://sonarcloud.io \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
