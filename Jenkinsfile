properties([pipelineTriggers([githubPush()])])

node('linux') { 
    stage('Unit Tests') 
    {
        git 'https://github.com/Saad-999/java-project.git'
        sh 'ant -f test.xml -v' 
    }
    
    stage('Build') { 
        sh 'ant -f build.xml -v'
    }
    
    stage('Deploy') 
    {
        sh 'aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://seis665-assignment-10/' 
    }
    
    stage('Report') 
    {
        sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
    }
}
