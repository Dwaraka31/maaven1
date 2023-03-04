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
                deploy adapters: [tomcat9(credentialsId: 'aa4862d1-971e-40d4-a340-45c7b66025af', path: '', url: 'http://172.31.31.218:8080')], contextPath: 'dtest1', war: '**/*.war'
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
                deploy adapters: [tomcat9(credentialsId: 'aa4862d1-971e-40d4-a340-45c7b66025af', path: '', url: 'http://172.31.19.81:8080')], contextPath: 'dprod1', war: '**/*.war'
            }
        }
    }
    
}
