
pipeline {
    agent any
    parameters {
        choice(name :'Envirenment', choices :[
                       'STG',
                       'DEV',
                       'QA',
                       'UI'
                     ],
                     description : "Select the Envirenment"

                     )
         choice(name :'Headless', choices :[
                        'True',
                        'False'

                      ],
                      description : "Select the Headless Browser"

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
        choice(name :'tag', choices :[
                       '@regression',
                       '@sanity',
                       '@smoke' ,
                       '@orderEvent',
                       '@loadTesting'
                     ],
                     description : "Select the Feature Tag"

                     )
        string(defaultValue: '2', description: 'Implicite wait time', name: 'Implicite Wait Time:')
        string(defaultValue: 'testkarim1980@gmail.com', description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Runing tests suit'){
            steps{
                echo "The testing Environment is : ${Envirenment} "
                echo "The testing Browser is : ${Browsers} "
                echo "Headless Browser : ${Headless} "
                echo "The runing Tag is : ${tag}"
                sh "mvn test -Dcucumber.filter.tags=${tag}"
               // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
                echo "The application testing en ${Env} Environment, ${Browsers} Browser and Tag ${tag} was performed successfully"
                }
         }
    }

      post {
        always {
            echo "Test succeeded"

                     emailext (from:'testkarim1980@gmail.com',
                               to: "${notification_email}",
                               subject: "Email report '${JOB_NAME} ${BUILD_NUMBER}'",
                               body: readFile("target/reports/cucumber-reports/cucumber.html"),
                               mimeType:'text/html');


                     //to: env.notification_email)

//                 emailext (body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
//                      from: 'testkarim1980@gmail.com',
//                      subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
//                      //to: env.notification_email)
//                      to: "${notification_email}")
                      //cucumber fileIncludePattern: '/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'

            //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/extent-reports/SparkReport', reportFiles: 'Spark.htmld.html', reportName: 'Spark Test Report', reportTitles: ''])
            //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/cucumber-reports', reportFiles: 'cucumber.html', reportName: 'Spark Test Report', reportTitles: ''])
        }
      }

}


// pipeline {
//     agent any
//     parameters {
//         choice(name :'Env', choices :[
//                        'STG',
//                        'DEV',
//                        'QA',
//                        'UI'
//                      ],
//                      description : "Select the Envirenment"
                     
//                      )
//         choice(name :'tag', choices :[
//                        '@regression',
//                        '@sanity',
//                        '@smoke' ,
//                        '@orderEvent'
//                      ],
//                      description : "Select the Feature Tag"
                     
//                      )
//         string(defaultValue: '2', description: 'Implicite wait time', name: 'Implicite Wait Time:')
//         string(defaultValue: 'testkarim1980@gmail.com', description: 'email for notifications', name: 'notification_email')
//     }

//     stages {
//          stage('Runing tests suit'){
//             steps{
//                 echo "${tag} Testing"
//                 sh "mvn test -Dcucumber.filter.tags=${tag}"
//                // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
//                 echo "The ${tag} was performed"
//                 }
//          }
//     }

//       post {
//         always {
//             echo "Test succeeded"
            
//                      emailext (from:'testkarim1980@gmail.com',
//                                to: "${notification_email}",
//                                subject: "Email report '${JOB_NAME} ${BUILD_NUMBER}'",
//                                body: readFile("target/reports/cucumber-reports/cucumber.html"),
//                                mimeType:'text/html');
                               
                               
//                      //to: env.notification_email)
                     
// //                 emailext (body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
// //                      from: 'testkarim1980@gmail.com',
// //                      subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
// //                      //to: env.notification_email)
// //                      to: "${notification_email}")
//                       //cucumber fileIncludePattern: '/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'
            
//             //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/extent-reports/SparkReport', reportFiles: 'Spark.htmld.html', reportName: 'Spark Test Report', reportTitles: ''])
//             //publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '../target/reports/cucumber-reports', reportFiles: 'cucumber.html', reportName: 'Spark Test Report', reportTitles: ''])
//         }
//       }
        
// }
