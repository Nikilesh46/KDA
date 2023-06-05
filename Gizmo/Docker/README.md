Installation Instructions:



######Set up the repository######

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

######Add Docker’s official GPG key#######

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg


######Use the above setup Repository######

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
###### Install Docker Engine #######

###Update package###

sudo apt-get update

### Install Docker Enginer, ContainerD and Docker Compose ###

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

##### Configs ######

service docker restart
sudo usermod -aG docker $USER
newgrp docker
sudo chmod 666 /var/run/docker.sock
sudo systemctl restart docker 


###Verify###

sudo docker run hello-world


