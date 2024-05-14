pipeline {
    agent {
        label 'slave'
    }
    
    stages {

        // stage('Build') {
        //     steps {
        //         script {
        //             sh 'mvn clean install'
        //         }
        //     }
        // }

        // stage('Test') {
        //     steps {
        //         script {
        //             sh 'mvn test'
        //         }
        //     }
        // }

        // stage('Package') {
        //     steps {
        //         script {
        //             sh 'mvn package'
        //         }
        //     }
        // }

        // stage('Publish Artifact') {
        //     steps {
        //         script {
        //             archiveArtifacts "target/*.jar"
        //         }
        //     }
        // }

        stage('Sonar') {
            steps {
                script {
                    sh """
                        ./gradlew sonarqube
                    """
                }
            }
        }        

    }

    post {
        success {
            echo 'Build successful! Artifact generated and published.'
            jacoco(
                execPattern: 'build/jacoco/*.exec',
                classPattern: 'build/classes',
                sourcePattern: 'src/main/java'
            )
            publishHTML (target : [allowMissing: false,
                            alwaysLinkToLastBuild: true,
                            keepAll: true,
                            reportDir: 'build/reports/jacoco/test/html',
                            reportFiles: 'index.html',
                            reportName: 'Jacoco',
                            reportTitles: 'sonarqube-jacoco-code-coverage'])
        }
    }
}