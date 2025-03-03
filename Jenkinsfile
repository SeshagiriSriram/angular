pipeline {
    agent any
    stages {
stage("Restore npm packages") {
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

	 stage('setup') {
	  parallel { 
            steps {
                sh 'npm install'
            }
	    steps { 
		sh 'vagrant plugin install virtualbox_WSL2' 
		} 
         } 
        }

	stage('build') { 
		steps { 
			sh 'ng build' 
		} 
	} 

	stage('test') { 
		steps { 
			echo 'in a normal case, setup an env with Chrome browsers etc and run in ||' 
		} 
	} 
	stage ('Deploy Infra') { 
		steps {
		sh 'vagrant up' 
		} 
	}

	stage ('Deploy infra') { 
		steps { 
		sh 'sudo cp -r dist /var/www/html/app' 
		} 
	} 
 
        }
    }
}
