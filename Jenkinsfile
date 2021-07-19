
pipeline {
    agent any
    parameters {
        choice(choices['@regression',
                       '@sanity',
                       '@smoke'
                     ],
                     description: "Select the Feature Tag",
                     name: 'tag'
                     )
        string(defaultValue: "karimmekdoud@gmail.com", description: 'email for notifications', name: 'notification_email')
    }

    stages {
         stage('Smoke Testing'){
          steps{
      echo 'Smoke Testing'

                }
        }
   
   }
}
