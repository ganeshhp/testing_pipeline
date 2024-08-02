def notify(status) {
  mail (
        body:"""${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
                 Check console output at, 
                 href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]""",
        cc: '<valid-email-id>', 
        subject: """JenkinsNotification: ${status}:""", 
        to: '<alid-email-id>'  
       ) 
 }


node ('build_server') {

    notify ('starting_job ${env.JOB_NAME}')

    stage ('SCM_checkout') {
        checkout scmGit(branches: [[name: '*/master']], 
            extensions: [], 
            userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']])
    }  

    stage ('app-build') {
        sh 'mvn clean package'
    }
    
    notify ('approval_for_deployment_needed')
    
    input 'Please provide Approval for deployment to artifactory'
    
    stage ('delpoy_to_artifactory') {
        sh 'curl -uganeshhp@gmail.com:cmVmdGtuOjAxOjE3NTM5MzkxMzI6WjJLUjhnaGVrS0MxOTNkVnplTDVwZmE5R0dn -T target/*.war "https://ganesh310724.jfrog.io/artifactory/project10-generic-local/petclinic.war"'
    }
}
