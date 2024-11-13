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


