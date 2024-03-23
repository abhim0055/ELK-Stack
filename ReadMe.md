This file explains steps involved in intsllating the ELK stack in your local machine using docker-compose file


STEP 1 :   update local databases of available packages (local package index) on your system 

    sudo apt-get update

STEP2: Install docker and docker compose using apt

Step 2.1 : Docker Installation on Ubuntu 22.04
    
    #Remove conflicting packages if they are already existing
    
    for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

    #Setup docker apt Repository

    # Add Docker's official GPG key:
    
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    
    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    
    #Install Docker Packages
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    #Verify docker Installations
    sudo docker run hello-world

Step 2.2 : Docker-Compose Installation on Ubuntu 22.04
    sudo apt-get install docker-compose 

STEP 3:  Create folders elk & inside elk create logstash on your current working directory(work space) 
    sudo mkdir -p elk/logstash

STEP 4: create a logstash.conf file inside logstash and copy below mentioned content
    sudo vi logstash.conf
    #Paste the below content
    ################################################
      input {
          file {
              path => "/your/work/dir/temp/inlog.log"
          }
      }
      
      output {
          elasticsearch {
              hosts =>["http://elasticsearch:9200"]
          }
      }
    ##################################################
    
STEP 5: Create a docker-compose.yml file in the elk directory (/your/work/dir/elk/docker-compose.yml)
    sudo vi docker-compose.yml
    Copy the content present in the docker-compose.yml file added in the repo
    
    
