
pipeline {
    agent any
            choice(name: 'tag',
                   choices['@regression',
                          '@sanity',
                          '@smoke'
                         ],
                     description: "Select the Feature Tag"
                     )

    stages {
         stage('Smoke Testing'){
          steps{
      echo 'Smoke Testing'

                }
        }
   
   }
}
