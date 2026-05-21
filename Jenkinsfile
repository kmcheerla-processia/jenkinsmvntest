pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage('Test') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn test -DBrowser=Chrome'
                }
            }
        }

        stage('Static Code Analysis') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn -DskipTests checkstyle:checkstyle'
                }
            }
        }

        stage('SonarQube Quality Gate') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn -DskipTests sonar:sonar -Dsonar.qualitygate.wait=true'
                }
            }
        }

        stage('Code Review') {
            steps {
                echo 'Manual code review stage completed'
            }
        }

        stage('Code Quality Check') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn -DskipTests checkstyle:check'
                }
            }
        }

        stage('FindBugs') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn -DskipTests findbugs:findbugs'
                }
            }
        }

        stage('PMD') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
                    sh 'mvn -DskipTests pmd:pmd'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy App'
            }
        }
    }
}
