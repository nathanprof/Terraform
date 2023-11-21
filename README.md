# Working-with-Terraform
Using terraform in my VMware Ubuntu Linux to create templates of resources in the cloud and on-premises
# Install Terraform
- sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
- wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
- gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
- echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
- sudo apt update
- sudo apt-get install terraform
# Verify the installation
- terraform -help (lists the terraform available commands)
- terraform -help plan (this tells you what the subcommand plan does and available options)
- terraform -install-autocomplete (install the autocomplete package)
# Using terraform to create an nginx server in a docker container
- Note: you must have docker installed already
- systemctl status docker (to verify you have docker installed )
## docker installation in case you don't already have
- ### Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
### Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
- sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
- sudo usermod -aG docker $USER && newgrp docker
- systemctl enable docker
- systemctl start docker
- systemctl sattus docker
