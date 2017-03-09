pipeline {
	agent any

	stages{
		stage('build & unit tests') {
	  		agent { label 'build' }
	  		steps {
	  			sleep 5
	  		}
		}
		stage('static analysis') {
	  		agent { label 'build' }
	  		steps {
	  			sleep 5
	  		}
		}
		stage('acceptance tests') {
			steps {
		  		parallel(
		  			chrome : {
				  			sleep 5
			        }, edge : {
				  			sleep 5
			        }, firefox : {
				  			sleep 5
			        }
			  	)
			}
		}
		stage('staging') {
	  		steps {
	  			sleep 5
	  		}
		}
		stage("manual approval") {
        	steps {
        		input("Attation à keskeu tu fé ! ça part en prod mec!")
        	}
    	}
    	stage('deploy') {
	  		steps {
	  			sleep 5
	  		}
		}
	}
}

