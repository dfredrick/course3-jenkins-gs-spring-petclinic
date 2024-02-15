
pipeline {
    agent any
    
    environment {
        JAVA_HOME = "/Users/dfredrick/Downloads/openjdk_17.0.10_17.48.16_aarch64"
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
    
    stages {
        stage("checkout") {
            steps {
                git branch:'main', url: 'https://github.com/dfredrick/course3-jenkins-gs-spring-petclinic'
            }
        }
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        
        
        stage("capture") {
            steps {
                // **/target/*.jar
                archiveArtifacts artifacts: '**/target/*.jar'
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
    post {
        always {
            emailext body: "${env.BUILDURL}\n${currentBuild.absoluteUrl}", 
            subject: "${currentBuild.currentResult}",
            to: 'always@foo.bar'
        }
    }
}

