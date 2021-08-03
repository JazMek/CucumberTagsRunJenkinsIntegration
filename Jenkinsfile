
pipeline {
    agent any
    parameters {
        choice(name :'Env', choices :[
                       'DEV',
                       'QA',
                       'UI'
                     ],
                     description : "Select the Envirenment"
                     
                     )
        choice(name :'tag', choices :[
                       '@regression',
                       '@sanity',
                       '@smoke' ,
                       '@orderEvent'
                     ],
                     description : "Select the Feature Tag"
                     
                     )
        string(defaultValue: 'karimmekdoud@gmail.com', description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Smoke Testing'){
            steps{
                echo "${tag} Testing"
                sh "mvn test -Dcucumber.filter.tags=${tag}"
               // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
                echo "The ${tag} was performed"
                }
         }

//                              post {
//         success {
//             echo "Test succeeded"
//             script {
//                 mail(bcc: '',
//                      body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
//                      cc: '',
//                      from: 'jenkins-admin@gmail.com',
//                      replyTo: '',
//                      subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
//                      //to: env.notification_email)
//                      to: "${notification_email}")
//                       cucumber fileIncludePattern: '**/CucumberTagsRunJenkinsIntegration/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'
//                       publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
//              }
//          }
                         
//      }

//         failure {
//             echo "Test failed"
//           script {
//             mail(bcc: '',
//                 body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
//                  cc: '',
//                  from: 'jenkins-admin@gmail.com',
//                  replyTo: '',
//                  subject: "${JOB_NAME} ${BUILD_NUMBER} failed",
//                  to: env.notification_email)
//                  cucumber fileIncludePattern: '**/CucumberTagsRunJenkinsIntegration/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'
//                  publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/tester/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
//           }
//         }
       
            post {
        always {
            echo "E mail sent to ${notification_email}"
            
//             emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
//                      recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
//                      to: "${notification_email}",
//                      subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
            mail bcc: '', body: 'the build was sects', cc: 'email notification', from: '', replyTo: '', subject: 'Email notification', to: 'karimmekdoud@gmail.com'
            
        }
    }
   
   }
}
