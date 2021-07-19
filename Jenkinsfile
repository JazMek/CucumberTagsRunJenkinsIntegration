
pipeline {
    agent any
            choice(choice['@regression',
                          '@sanity',
                          '@smoke'
                         ],
                     description: "Select the Feature Tag",
                     name: 'tag'
                     )

    stages {
         stage('Smoke Testing'){
          steps{
      echo 'Smoke Testing'

                }
        }
   
   }
}
