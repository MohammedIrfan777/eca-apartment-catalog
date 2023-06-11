pipeline {
    environment {
        REGISTRY_NAME = "khazi123/ecaapartmentcatalog"
     }

    agent any
    tools {
        maven "MAVEN_HOME"
    }
    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                    git branch: 'main', url: 'https://github.com/MohammedIrfan777/eca-apartment-catalog.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install -DskipTests"
            }
        }

         stage('Test & Code Coverage') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
             post {
                success {
                     archiveArtifacts 'target/*.jar'
                     junit 'target/surefire-reports/*.xml'
                     jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }

        stage('SonarQube') {
                  environment {
                    scannerHome = tool 'SonarQube'
                  }
                  steps {
                              script {
                              sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ecausermgmt: \
                                                                  -Dsonar.projectName=ecausermgmt \
                                                                  -Dsonar.projectVersion=1.0 \
                                                                  -Dsonar.sources=src/ \
                                                                  -Dsonar.java.binaries=target/classes/com/ps/mslife/controller/ \
                                                                  -Dsonar.junit.reportsPath=target/surefire-reports/ \
                                                                  -Dsonar.jacoco.reportsPath=target/jacoco.exec"
                                                                  }
                                    }
             }

        stage('Building image') {
          steps{
            sh 'docker build -t $REGISTRY_NAME:$BUILD_NUMBER .'
          }
        }

        stage('Docker Build & Push') {
            steps {
                 sh 'docker push $REGISTRY_NAME:$BUILD_NUMBER'
            }
        }
    }

    post {
       always {
           deleteDir()
       }
   }
}
