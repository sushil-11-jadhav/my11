pipeline {
	agent {
		label {
			label "built-in"
			customWorkspace "/mnt/welcome"
		}
	}
	stages {
		stage ("docker started") {
			steps {
				sh "service docker start"
				
			}
		}		
		stage ("docker httpd run on JM") {
			steps {
					sh "rm -rf /mnt/welcome/*"
					sh "docker kill server1"
					sh "docker system prune -a -f"
					sh "docker run -dp 80:80 --name server1 httpd"
					sh "git clone https://github.com/sushil-11-jadhav/9-may.git -b 23Q1"
					sh "chmod -R 777 /mnt/welcome/9-may/index.html"
					sh "docker cp /mnt/welcome/9-may/index.html server1:/usr/local/apache2/htdocs"
			}
		}
		stage ("docker httpd run on slave") {
			agent {
				label {
					label "slave"
					customWorkspace "/mnt/slj"
				}
			}	
			steps {
					sh "rm -rf /mnt/slj/*"
					sh "docker kill server2"
					sh "docker system prune -a -f"
					sh "service docker start"
					sh "rm -rf /mnt/slj/*"
					sh "docker run -dp 90:80 --name server2 httpd"
					sh "git clone https://github.com/sushil-11-jadhav/9-may.git -b 23Q2"
					sh "chmod -R 777 /mnt/slj/9-may/index.html"
					sh "docker cp /mnt/slj/9-may/index.html server2:/usr/local/apache2/htdocs"
			}
		}
		stage ("docker httpd run on slave ssh") {
			agent {
				label {
					label "slave ssh"
					customWorkspace "/mnt/sls"
				}
			}
			steps {
					sh "sudo rm -rf /mnt/sls/*"
					sh "sudo docker kill server3"
					sh "sudo docker system prune -a -f"
					sh "sudo service docker start"
					sh "sudo rm -rf /mnt/sls/*"
					sh "sudo docker run -dp 8081:80 --name server3 httpd"
					sh "sudo git clone https://github.com/sushil-11-jadhav/9-may.git -b 23Q3"
					sh "sudo chmod -R 777 /mnt/sls/9-may/index.html"
					sh "sudo docker cp /mnt/sls/9-may/index.html server3:/usr/local/apache2/htdocs"
			}
		}
	}	
}		
