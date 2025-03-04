pipeline {
    agent any
    stages {
stage("Restore npm Packages") {
    steps {
        writeFile file: "next-lock.cache", text: "$GIT_COMMIT"
 
        cache(caches: [
            arbitraryFileCache(
                path: "node_modules",
                includes: "**/*",
                cacheValidityDecidingFile: "package-lock.json"
            )
        ]) {
            sh "npm install"
        }
    }
}

	 stage('Setup Environment') {
	  parallel { 
	   stage('npm Install') { 
            steps {
                sh 'npm install'
            }
            } 
           stage('Vagrant Env. Setup for Infra'){ 
	    steps { 
		sh 'vagrant plugin install virtualbox_WSL2' 
                sh 'vagrant plugin install vagrant-scp'
		} 
           } 
         } 
        }

	stage('Build the Application') { 
		steps { 
			sh 'ng build --configuration production'
		} 
	} 

	stage('App. Testing') 
		steps { 
			echo 'in a normal case, setup an env with Chrome browsers etc and run in ||' 
		} 
	} 
	stage ('Deploy Infra') { 
		steps {
		sh 'vagrant up' 
		} 
	}

	stage ('Deploy App on Instra') { 
		steps { 
		echo 'All done'
		} 
	} 
 
        }
    }
