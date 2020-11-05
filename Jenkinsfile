
node
{
    def mavenhome = tool name: "Maven3.6.3"
    stage('CheckoutCode')
    {
        git credentialsId: 'c5ccaad3-18ad-4d21-9261-e845b8cbf7b0', url: 'https://github.com/Sunilpractise/maven-standalone-application.git'
    }
    stage('Build')
    {
        sh "$mavenhome/bin/mvn clean package"
    }
    stage('Execute sonaQube report')
    {
        sh "$mavenhome/bin/mvn clean package sonar:sonar"
    }
    stage('Artifact repo')
    {
        sh "$mavenhome/bin/mvn deploy"
    }
    stage('Deploy to tomcat')
    {
        sshagent(['d3a46f5a-39b3-48a3-89f5-9b658de299ef'])
        {
            sh "scp -o StrictHostKeyChecking=no target/maven-stanalone-application-0.0.1-SNAPSHOT.jar ec2-user@13.234.67.196:/opt/apache-tomcat-9.0.39/webapps/"
}
    }
     stage('Email Notification')
    {
       mail bcc: '', body: '''Build over 

Regards,
Sunil
''', cc: '', from: '', replyTo: '', subject: 'Email notification Build Over', to: 'sunil.aravind333@gmaiil.com'
    }
    
}
