
pipeline {
    agent any
    parameters {
        choice(name :'TestingEnvironment', choices :[
                       'STG',
                       'DEV',
                       'QA',
                       'UI'
                     ],
                     description : "Select the Testing Environment"

                     )
        
                choice(description : "Select the Operating System: " ,name :'OS', choices :[
                       'Windows',
                       'Mac',
                       'Linux',
                     ]
                
                     )
        
         string(description: 'Select the OS Version: ', defaultValue: 'Not defind', name: 'OS Version')
        
         choice(name :'Headless', choices :[
                        'False',
                        'True'
                      ],
                      description : "Headless Browser"

                      )
        choice(name :'Browsers', choices :[
                       'Chrome',
                       'Safari',
                       'Fire Fox',
                       'Internet Explorer',
                       'All'
                     ],
                     description : "Select the Browser"
                     )
        
        string(defaultValue: 'Not defind', description: 'Browser Version', name: 'Browser Version')
        
        choice(name :'tag', choices :[
                       '@regression',
                       '@sanity',
                       '@smoke' ,
                       '@orderEvent',
                       '@loadTesting'
                     ],
                     description : "Select the test suit using the corresponding Tag"
                     )
        string(defaultValue: '2', description: 'Implicitly wait time', name: 'Implicitly Wait Time:')
        string(defaultValue: 'testkarim1980@gmail.com', description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Running tests suit'){
            steps{
                echo "The testing Environment is : ${TestingEnvironment} "
                echo "The testing Browser is : ${Browsers} "
                echo "Headless Browser : ${Headless} "
                echo "The running Tag is : ${tag}"
                sh "mvn test -Dcucumber.filter.tags=${tag}"
               // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
                echo "The application testing en ${TestingEnvironment} Environment, ${Browsers} Browser and Tag ${tag} was performed"
                }
         }
    }
//       post {
//         always {
//             echo "Test succeeded"
//                      emailext (from:'testkarim1980@gmail.com',
//                                to: "${notification_email}",
//                                subject: "Email report '${JOB_NAME} ${BUILD_NUMBER}'",
//                                body: readFile("/target/reports/cucumber-reports/cucumber.html"),
//                                cucumber (fileIncludePattern: '/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'),
//                                mimeType:('text/html'))
//                      //to: env.notification_email)
            
              post {
    always {
        
//        mail to: "${notification_email}",
//           subject: "Status of pipeline: ${currentBuild.fullDisplayName}",
//           body: "${env.BUILD_URL} has result:  ${currentBuild.result}"
        
        emailext attachmentsPattern: '**/*.html',
                 body: "${env.BUILD_URL} has result:  ${currentBuild.result}",
                 subject: "Status of pipeline: ${currentBuild.fullDisplayName}",
                 to: "${notification_email}"
        
        
        
        //emailext attachmentsPattern: '**/*.html', body: 'Body here', subject: 'Subject here', to: 'mail@gmail.com, mail2@gmail.com, mail3@gmail.com'
//         publishHTML (target: [
//       allowMissing: false,
//       alwaysLinkToLastBuild: false,
//       keepAll: true,
//       reportDir: 'api/build/reports/test',
//       reportFiles: 'index.html',
//       reportName: "API Unit Testing Results"
//     ])
        
      publishHTML (target: [
      allowMissing: false,
      alwaysLinkToLastBuild: false,
      keepAll: true,
      reportDir: 'target/reports/cucumber-reports',
      reportFiles: 'cucumber.html',
      reportName: "Cucumber Reports Results"
    ])
//     }
//   }

//                 emailext (body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
//                      from: 'testkarim1980@gmail.com',
//                      subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
//                      //to: env.notification_email)
//                      to: "${notification_email}")
                      //cucumber fileIncludePattern: '/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'

            // publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/extent-reports/SparkReport', reportFiles: 'Spark.htmld.html', reportName: 'Spark Test Report', reportTitles: ''])
            //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/cucumber-reports', reportFiles: 'cucumber.html', reportName: 'Spark Test Report', reportTitles: ''])
                
//         cucumber buildStatus: 'UNSTABLE',
//                 failedFeaturesNumber: 1,
//                 failedScenariosNumber: 1,
//                 skippedStepsNumber: 1,
//                 failedStepsNumber: 1,
//                 classifications: [
//                         [key: 'Commit', value: '<a href="${GERRIT_CHANGE_URL}">${GERRIT_PATCHSET_REVISION}</a>'],
//                         [key: 'Submitter', value: '${GERRIT_PATCHSET_UPLOADER_NAME}']
//                 ],
//                 reportTitle: 'Cucumber Report',
//                 fileIncludePattern: '**/*cucumber-report.json',
//                 sortingMethod: 'ALPHABETICAL',
//                 trendsLimit: 100
        }
      }

}
