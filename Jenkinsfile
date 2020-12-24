
pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    
    stages{
    stage("code checkout"){
        steps{
        sh "echo hello"
        }
    }
    stage ("code build"){
        steps{
        sh "mvn clean"
        }
    }
    stage("Unit test"){
        steps{
        sh "mvn test"
        }
    }
    }
    post{
        success{
            sh "echo success"
        }
    }
    
}
