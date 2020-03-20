pipeline {
   agent {
	  label "${params.slave_name}"
	}

   stages {
      stage('Clone') {
         steps {
      // Get some code from a GitHub repository
          checkout scm
         }
      }
      stage('Build') {
         steps {
            // Run Maven on a Unix agent.
		 sh "${params.build_cmd}"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }
      }
      stage('docker build') {
         steps {
             sh "docker build -t=saijyothi9/nginx ."
         }
      }
       stage('docker push') {
         steps {
             sh "docker push saijyothi9/nginx"
         }
      }
       stage('docker run') {
         steps {
             sh "docker stop \$(docker ps -a -q)"
			 sh "docker rm \$(docker ps -a -q)"
			 sh "docker run --name mynginx1 -p 80:80 -d saijyothi9/nginx"
         }
      }
        
   }
}
