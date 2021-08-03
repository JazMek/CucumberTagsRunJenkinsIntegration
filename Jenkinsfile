
pipeline {
    agent any
    parameters {
        choice(name :'Env', choices :[
                       'STG',
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
        string(defaultValue: '2', description: 'Implicite wait time', name: 'Implicite Wait Time:')
        string(defaultValue: 'testkarim1980@gmail.com', description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Runing tests suit'){
            steps{
                echo "${tag} Testing"
                sh "mvn test -Dcucumber.filter.tags=${tag}"
               // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
                echo "The ${tag} was performed"
                }
         }
    }

      post {
        always {
            echo "Test succeeded"
                emailext (body: "Run ${JOB_NAME}-#${BUILD_NUMBER} succeeded. To get more details, visit the build results page: ${BUILD_URL}.",
                     from: 'testkarim1980@gmail.com',
                     subject: "${JOB_NAME} ${BUILD_NUMBER} succeeded",
                     //to: env.notification_email)
                     to: "${notification_email}")
                      cucumber fileIncludePattern: '**/CucumberTagsRunJenkinsIntegration/target/reports/cucumber-reports/cucumber.json', sortingMethod: 'ALPHABETICAL'
                      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '/home/reports', reportFiles: 'reports.html', reportName: 'Performance Test Report', reportTitles: ''])
        }
      }
        
}
