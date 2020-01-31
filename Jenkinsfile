pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn clean compile'
                }
            }
        }
        
           stage('SonarQube analysis') {
      tools {
        sonarQube 'SonarQube Scanner 4.2'
      }
      steps {
        withSonarQubeEnv('SonarQube Scanner') {
          sh 'sonar-scanner'
        }
      }
    }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn test'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'maven_3_5_0') {
                    sh 'mvn deploy'
                }
            }
        }
    }
}
