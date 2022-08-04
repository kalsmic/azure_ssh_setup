# azure_ssh_setup

The purpose of this repository is to act as a guide for setting up a remote virtual machine to run aws tools and docker. This is aimed at giving windows users who might be limited interms of processing power and bandwidth to run docker resources.

How to run the setup
Set the 
```bash
  sh setup.sh
 ```
 
## Break down of the setup file
### Install Tools
```bash
  sudo apt install zip unzip
```
### Setup Github
Replace your name , username and email
```bash
  git config --global user.name "Firstname Lastname"
  git config --global user.email "yourmain@provider.com"
  git config --global user.username "gitusername"
  git config --global init.defaultBranch main
```

### Install Docker
```bash
  sudo apt install apt-transport-https ca-certificates curl software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
  sudo apt update
  apt-cache policy docker-ce
  sudo apt install -y docker-ce
  sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose
  sudo groupadd docker
  sudo usermod -aG docker $USER
```
### Install AWScli
```bash
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
```
### Install eksctl
```bash
  curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
  sudo mv /tmp/eksctl /usr/local/bin
```
### Install Kubectl
```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
  echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
  sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
  chmod +x kubectl
  mkdir -p ~/.local/bin
  mv ./kubectl ~/.local/bin/kubectl
```

## command to run on your local machine in a Bash environment

### Add your local public key to your remote vm authorized keys for auto login
```bash
 cat ~/.ssh/id_ed25519.pub | ssh -i ~/.ssh/azure_private_key.pem user@host 'cat >> ~/.ssh/authorized_keys'
 ```


## How to generate SSH KEYS
[Folow this link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
