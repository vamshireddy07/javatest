pipeline {
    agent any

    tools{
        maven 'maven'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo "${env.BUILD_NUMBER}"
                echo "${env.BUILD_URL}"
            }
        }

        stage('Code Quality') {
            steps {
                echo 'Quality'
            }
        }

        stage('Deploy to Dev') {
            steps {
                echo 'Dev'
            }
        }

         stage('Deploy to Test') {
            steps {
                script{
                    if (env.BRANCH_NAME =="develop" || env.BRANCH_NAME =="master")
                }
                echo 'Test'
            }
        }

         stage('Deploy to UAT') {
            steps {
                echo 'UAT'
            }
        }

         stage('Deploy to Pre_Prod') {
            steps {
                echo 'Staging'
            }
        }

        stage('Prod Approval'){
            steps{
                script{
                    if (env.BRANCH_NAME =="master"){
                    input('Proceed for Prod Depolyment')
                    }
                }
            }
        }

         stage('Deploy to Prod') {
            steps {
                script{
                    if (env.BRANCH_NAME =="master")
                echo 'Prod'
                }
            }
         }

            post{
                failure{
                    echo 'sending Notification'
                }
            }
               post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
             mail to: 'team@example.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
        }
        changed {
            echo 'Things were different before...'
        }
        
    }


}