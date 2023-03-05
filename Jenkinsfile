pipeline
{
    agent any
    stages
    {
        stage('continuousDownload')
        {
            steps
            {
                git 'https://github.com/Dwaraka31/maaven1.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousDeployment')
        {
            steps
            {
              sh '''scp /var/lib/jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.31.218:/var/lib/tomcat9/webapps/testapp.war'''
            }
        }
        stage('continuouTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('continuousDelivery')
        {
            steps
            {
                input message: 'Approval for deplyoment', submitter: 'Dwaraka'
                sh '''scp  /var/lib/jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.19.81:/var/lib/tomcat9/webapps/prodapp.war'''
            }
        }
    }
    
}
