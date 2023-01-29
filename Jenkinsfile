pipeline {
    agent any
    // set a trigger to run this daily 5:30 utc Time
    
	triggers {
        
		cron('H/2 * * * *')
    
	}
    environment {
	    //Version="product"
	    Repo="${params.Choice}"
	    Branch="${params.Branch}"
	    CredentialID="github_ID"
	  
    }
  
    parameters {
		choice(name: 'Choice', choices: ['padminiyepuri/docker_pipelines'], description: 'Choice repository to build')
		choice(name: 'Branch', choices: ['master', 'dev'], description: 'Choice branch to build')
    }
    
    stages {
        stage('checkout repo') {
            steps {
    		    checkout changelog: true, poll: false, scm: [$class: 'GitSCM', branches: [[name: "*/$Branch"]], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: "docker_pipelines"], [$class: 'SubmoduleOption', disableSubmodules: true, parentCredentials: false, recursiveSubmodules: false, reference: '', timeout: 3000, trackingSubmodules: false]], submoduleCfg: [], userRemoteConfigs: [[credentialsId: "$CredentialID", url: "https://github.com/padminiyepuri/docker_pipelines.git"]]]
            }
        }    
	   stage('Build code') {
	       steps {
	            sh 'script.sh'
				
			}
		}
    }
}

}
