node
{
    try
		{
			
			//Download code from stash  
    		stage'download_stash_code'
				download_stash_code()
			//perform maven clean 
    		stage'clean'
				clean()
			//perform maven munit tests     	
			stage'munit_tests'
				munit_tests()

			//perform maven munit tests     	
			stage'sonar_tests'
				sonar_tests()

			stage'deploy_to_artifactory'
				push_to_artifactory()
		
		}
	catch(e) 
		{
		currentBuild.result = "FAILED"	
		throw(e)
		} 
    finally 
		{
			print "done"
		}	
}	
	
// Function definitions start from here 
	
//Function definition for downloading code from Stash to workspace in jenkins 	
def download_stash_code()
	{
	
	checkout scm
	}		
//Function definition to perform maven clean 
def clean()
	{
	sh "mvn clean"
	} 
//Function definition to perform maven tests 	
def munit_tests()
	{
	sh "mvn test"  
	}
//Function definition to perform sonar tests 
def sonar_tests()
{
	sh "mvn clean sonar:sonar"
}
//Function definition to perform artifactory deploy 
def push_to_artifactory()
{
	sh "mvn deploy"
}







	


	


	
	
	 
