# EKS creation script guidelines
## First we need to install required pakages that we need for this script to run successfully.
#### Install basic dependencies
```
sudo apt install curl
sudo apt-get install jq
```
#### check awscli version
```
aws --version
```

#### if cli version is v1.x.x, than use below commands to upgrade the awscli to v2.x.x
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
sudo ln -s /usr/local/aws-cli/v2/current/bin/aws /usr/local/bin/aws
aws --version
```
#### Install kubectl version 1.21.0 as the latest one are not compatible for eks awscli.
```
curl -LO "https://dl.k8s.io/release/v1.21.0/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version --client
```
#### Install eksctl version v0.194.0
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/v0.194.0/eksctl_Linux_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```
#### Install aws-iam-authenticator dependecy
```
curl -o aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.7/aws-iam-authenticator_0.5.7_linux_amd64
chmod +x aws-iam-authenticator
sudo mv aws-iam-authenticator /usr/local/bin/
aws-iam-authenticator
```
## Setup your user as a default for awscli.
### We need to setup a user who have systemAdministrator access as a default. 
#### First see if there is already any user access keys are setup as default
```
cd
cat .aws/credentials
cat .aws/config
```
#### Output
![image](https://github.com/user-attachments/assets/968a59db-723a-49bb-8d2c-8440b9e74e93)
If you see any user already setup as default, than we have two option if you want to use this user than please make sure these access keys belongs to the user of your infra otherwise remove these configuration by using below code (only remove deault one).
```
nano .aws/credentials
nano .aws/config
```
## Setup the script.sh file according to yourself.
#### Add CLUSTER_NAME, REGION and NODE_GROUP_NAME in the variable section location at the top of the script. Please dont use micro and small instance type for this setup as these don't fulfill our setup needs.
![image](https://github.com/user-attachments/assets/5f65c903-bb3e-48e4-88b3-a58370aa481f)




