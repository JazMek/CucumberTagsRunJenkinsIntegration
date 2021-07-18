pipeline {
    agent any
    parameters {
        choice(choices: 'yes\nno', description: 'Are you sure you want to execute this test?', name: 'run_test_only')
        choice(choices: 'yes\nno', description: 'Archived war?', name: 'archive_war')
        string(defaultValue: "mig.suarez1989@gmail.com", description: 'email for notifications', name: 'notification_email')
    }
    environment {
        firstEnvVar= 'FIRST_VAR'
        secondEnvVar= 'SECOND_VAR'
        thirdEnvVar= 'THIRD_VAR'
    }
    stages {
        stage('Test'){
            when {
                environment name: 'run_test_only', value: 'yes'
            }
            steps{
                sh 'cd examples/java-calculator && mvn clean integration-test'
            }
        }

        stage ('Run demo parallel stages') {
        steps {
        parallel(
        "Parallel stage #1":
                  {
                  //running a script instead of DSL. In this case to run an if/else
                  script{
                    if (env.run_test_only =='yes')
                        {
                        echo env.firstEnvVar
                        }
                    else
                        {
                        echo env.secondEnvVar
                        }
                  }
         },
        "Parallel stage #2":{
                echo "${thirdEnvVar}"
                }
                )

             }
        }


    }

    post {
        success {
        //node('node1'){

            echo "Test succeeded"
            script {

                mail(bcc: '',
                     body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
                     cc: '',
                     from: 'jenkins-admin@gmail.com',
                     replyTo: '',
                     subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
                     to: env.notification_email)
                     if (env.archive_war =='yes')
                     {
                        archiveArtifacts '**/java-calculator-*-SNAPSHOT.jar'
                      }
                      cucumber fileIncludePattern: '**/java-calculator/target/cucumber-report.json', sortingMethod: 'ALPHABETICAL'
            //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
            }
        //}
        }
        failure {
            echo "Test failed"
            mail(bcc: '',
                body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
                 cc: '',
                 from: 'jenkins-admin@gmail.com',
                 replyTo: '',
                 subject: "${JOB_NAME} ${BUILD_NUMBER} failed",
                 to: env.notification_email)
                 cucumber fileIncludePattern: '**/java-calculator/target/cucumber-report.json', sortingMethod: 'ALPHABETICAL'

            //publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/tester/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
        }
    }

}
