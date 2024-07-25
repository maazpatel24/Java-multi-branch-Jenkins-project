pipeline {
    agent any

    stages {
        // stage('Checkout') {
        //     steps {
        //         // Checkout code from Git repository
        //         git credentialsId: 'git-access', url: 'https://github.com/maazpatel24/DevOpsClassCode.git', branch: env.BRANCH_NAME
        //     }
        // }
        // stage ('Compile Stage') {

        //     steps {
        //         withMaven(maven : 'Maven-3.9.0') {
        //             sh 'mvn clean compile'
        //         }
        //     }
        // }
        // stage ('Testing Stage') {

        //     steps {
        //         withMaven(maven : 'Maven-3.9.0') {
        //             sh 'mvn test'
        //         }
        //     }
        // }
        // stage ('Deployment Stage') {
        //     steps {
        //         withMaven(maven : 'Maven-3.9.0') {
        //             sh 'mvn deploy'
        //         }
        //     }
        // }
        stage('Build') {
            steps {
                script {
                    // echo "Building in branch: ${env.BRANCH_NAME}"
                    withMave(maven: 'Maven-3.9.0') {
                        // Clean and compile the Maven project
                        sh 'mvn clean compile'
                    }
                }
            }
        }
        stage('Run') {
            steps {
                // echo "Runing in branch: ${env.BRANCH_NAME}"
                 // Execute the Java application
                withMave(maven: 'Maven-3.9.0') {
                    sh 'mvn exec:java -Dexec.mainClass="com.example.App"'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                // Archive the built artifacts
                archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
            // Clean up workspace
            cleanWs()
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}