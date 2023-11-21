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
## Docker installation in case you don't already have
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
- sudo systemctl enable docker (enables it to start at boot time)
- sudo systemctl start docker (starts the docker service)
- sudo systemctl status docker (checks the status of the docker service)
## Using terraform to create nginx server
- mkdir reggie-terrafoam-dock-tem (creates a directory)
- cd reggie-terrafoam-dock-tem (navigate into thedirectory)
- vim dock.tf (creates a file and paste contents in dock.tf into it by  pressing the key then after pasting press esc key then shift + :wq and press enter to exit and save)
- terraform plan (describes the changes Terraform will make to your infrastructure to bring it into the desired state specified by your configuration files)
- terraform init ( initialize a Terraform working directory)
- terraform apply -auto-approve (apply Terraform configuration changes without prompting for user confirmation note: risky in production you can leave the option out in production)
- docker ps (lists all running containers)
- http://192.168.4.132:8000/ or http://localhost:8000/ (to test the nginx server on the host as in the earlier command my vmware ip is 192.168.4.132 or locally in thevmare environment)
- terraform destroy -auto-approve (will automatically approve the destruction plan, bypassing the prompt for confirmation)
- docker images (to  view the docker images)
- docker rmi IMAGE_ID (to remove one or more images from your local Docker environment)
# Using terraform to create a resource-group in Ms Azure portal
## Prerequisites
- you must have an Azure subscription
- you must have az cli installed in your VMware workstation running ubuntu linux
- sudo apt install azure-cli (in case you don't have az cli installed, you can use this command to nstall it)
- curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash (in case you don't have az cli installed, you can use this command to nstall it)
### Creating the resource-group in azure portal using terraform
- mkdir terraform-rg
- cd terraform-rg
- vim main.tf (creates a file and paste contents in dock.tf into it by  pressing thei key then after pasting press esckey then shift + :wq and press enter to save and exit)
- terraform plan (describes the changes Terraform will make to your infrastructure to bring it into the desired state specified by your configuration files)
- terraform init ( initialize a Terraform working directory)
- terraform apply -auto-approve (apply Terraform configuration changes without prompting for user confirmation)
- terraform destroy -auto-approve (will automatically approve the destruction plan, bypassing the prompt for confirmation)
# Using terraform to create a linux vm in Ms Azure portal
- mkdir terraform-lin-vm
- cd terraform-lin-vm
- vim regtfvm.tf
- terraform plan
- terraform init 
- terraform apply -auto-approve 
- terraform destroy -auto-approve
# Using terraform to create a windows vm in Ms Azure portal
- mkdir terraform-win-vm
- cd terraform-win-vm
- vim regwintf.tf
- terraform plan
- terraform init 
- terraform apply -auto-approve 
- terraform destroy -auto-approve


