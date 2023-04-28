pipeline
{
    agent any
    stages
    {
        stage('continousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('continousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continousDeployement')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'd80c1ef9-edcc-4797-b4d3-46fb935eb432', path: '', url: 'http://172.31.26.176:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('continuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContinousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'db08985c-1307-41ef-9687-5545b8b2bb98', path: '', url: 'http://172.31.26.162:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
