pipeline {
	agent any

	stages{
		stage('build & unit tests') {
	  		agent { label 'build' }
	  		steps {
	  			withMaven(
        			maven: 'M3', 
        			mavenLocalRepo: '.repository') {
        			sh "mvn clean install"
        		}
        		stash name:"jar", includes:"target/\\*.jar"
	  		}
		}
		stage('static analysis') {
	  		agent { label 'build' }
	  		steps {
			    withSonarQubeEnv('Sonar') {
			       sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
			    }
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
	  			deleteDir()
	  			unstash "jar"
	  			sh 'ls -l target'
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
	  			deleteDir()
	  			unstash "jar"
	  			sh 'ls -l target'
	  			sleep 5
	  		}
		}
	}
}

