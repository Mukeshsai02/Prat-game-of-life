pipeline {
    agent any
	   environment 
	   {
		  sonar_url = 'http://172.31.4.216:9000/'
		  sonar_username = 'admin'
		  sonar_password = 'admin'
		  nexusUrl = '172.31.4.216:8081'
		  artifact_version = '0.0.1'

        }
    tools 
	{
		  // Install the Maven version configured as "M3" and add it to the path.
		  jdk 'Java8'
		  maven "Maven_3.3.9"
    }
	
	stages
    {
        stage('checkout') 
		{
          steps 
		  {
				// Get some code from a GitHub repository
				git branch: 'main', url: 'https://github.com/164411Prathyusha/Prat-game-of-life.git'
          }
        
        }
	    stage ('Compile and Build') 
		{
			 steps 
			 {
				   sh '''
				   mvn clean install -U  -Dmaven.test.skip=true 
				   '''
             }
	    }
	    
	  stage ('Docker build')
{  
     steps
 {
    sh '''
       docker build -t 164411/game-of-life-jenkins:v1 .
       '''
     }
}
    stage('Push docker image')
    {
        steps
   {
     sh '''
       docker login --username 164411 --password 1205@Ramya
       docker push 164411/game-of-life-jenkins:v1
      '''
        }  
    }
}
}
