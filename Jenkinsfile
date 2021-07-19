
pipeline {
    agent any
    parameters {
        choice(name :'tag', choices :['@regression',
                       '@sanity',
                       '@smoke'
                     ],
                     description : "Select the Feature Tag"
                     
                     )
        string(defaultValue: "karimmekdoud@gmail.com", description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Smoke Testing'){
          steps{
                echo '{tag} Testing'
                sh "mvn test -Dcucumber.filter.tags=${"tag"}"
               // sh 'mvn test -Dcucumber.options=”–tags ${tag}”'
                echo 'The {tag} was performed'


                }
        }
   
   }
}
