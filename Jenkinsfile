currentBuild.displayName = "Final_Demo # "+currentBuild.number

   def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }
        

pipeline{
        agent any  
        environment{
	    Docker_tag = getDockerTag()
        }
        
        stages{


              stage('building'){

               agent {
                docker {
                image 'maven'
                args '-v $HOME/.m2:/root/.m2'
                }
            }
                  steps{
                      script{
		    sh "mvn clean install"
                  }
                }  
              }



              stage('docker build')
                {
              steps{
                  script{
		 sh 'cp -r /home/ahamedbasha/.m2/target .'

                   sh 'docker build . -t ahamedbasha55/test:$Docker_tag'

			 {
				    
				  sh 'docker login -u ahamedbasha55 -p Allah786#'
				  sh 'docker push ahamedbasha55/test:$Docker_tag'
			}
                       }
                    }
                 }
	}	 	      
    
}
