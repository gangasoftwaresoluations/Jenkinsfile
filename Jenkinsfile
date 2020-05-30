node{
    def  mvnhome=tool name: 'maven3.6.1'
    
    
    
    stage("Checout")
    {
        git branch: 'development', credentialsId: '382ec160-103b-4758-9583-48c6764388d6', url: 'https://github.com/gangasoftwaresoluations/maven-web-application.git'
    }
    stage("Build")
    {
        sh "${mvnhome}/bin/mvn clean package"
    }
    stage("Generate Report")
    {
        sh "${mvnhome}/bin/mvn clean sonar:sonar"
    }
    stage(" Artifacts"){
        sh "${mvnhome}/bin/mvn  deploy"
    }
    
    stage("Deployment"){
    sshagent(['beff6cb3-b87a-42a5-98a8-c1ccad5654d8']) {
    sh "scp -o StrictHostKeyChecking=no target/*.war  ec2-user@13.235.115.41:/opt/apache-tomcat-9.0.35/webapps"
        }
    }
    
    stage("EmailNotification")
    {
            emailext body: '''HI,
    Build is Over

    Thanks,
    Gangadhar''', subject: 'Build Status', to: 'gangadharle403@gmail.com'
    }
}
