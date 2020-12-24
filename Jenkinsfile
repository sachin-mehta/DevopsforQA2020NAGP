
pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    
    stages{
    stage ('checkout')
		{
			steps
			{
				checkout scm
			}
		}
		stage ('Build')
		{
			steps
			{
				sh "mvn install"
			}
		}
		stage ('Unit Testing')
		{
			steps
			{
				sh "mvn test"
			}
		}
		stage ('Sonar Analysis')
		{
			steps
			{
				withSonarQubeEnv("Test_Sonar") 
				{
					sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar"
				}
			}
		}
	    stage ('Upload to Artifactory')
		{
			steps
			{
				rtMavenDeployer (
                    id: 'deployer',
                    serverId: '123456789@artifactory',
                    releaseRepo: 'sachin.nagpqa2020',
                    snapshotRepo: 'sachin.nagpqa2020'
                )
                rtMavenRun (
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: 'deployer',
                )
                rtPublishBuildInfo (
                    serverId: '123456789@artifactory',
                )
			}
		}
    }
    post{
        success{
            sh "echo success"
        }
    }
    
}
