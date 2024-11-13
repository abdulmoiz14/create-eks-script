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

## Final Things
#### How to run the script?
```
sh script.sh
```
#### How to get the IP and port use to curl or check it in the browser.
![image](https://github.com/user-attachments/assets/9978e8d5-96ee-40f2-bd3a-d8a12993612a)  
![image](https://github.com/user-attachments/assets/1a38ee8c-50af-4fd8-8805-a2b505134492)  
You'll see a line **Nginx is accessible at http://IP:PORT**. Hower your mouse on the link and ctrl+left click or copy it and then paste it to the browser to see the result.  
If the http is accessible it shows a line **OK: Nginx default page is displayed correctly.**  
If the http is not accessible it shows a line **Error: Nginx default page not displayed correctly.**
![image](https://github.com/user-attachments/assets/917906d3-d7b0-4d8b-9d46-2288f7d1ea74)  
#### Please dont quit or leave the cli when you see this line in cli "Cluster will start deleting after 3 minutes, please dont quit or exit from this CLI". This will delete all configuration automatically after 3 minutes.  
![image](https://github.com/user-attachments/assets/8a617d1d-886d-41bf-95a5-ad3a375fbd58)
#### If you accidently quit or leave the CLI then use the below command to delete the configuration otherwise it is hectic for you to remove all these things.
```
eksctl delete cluster --name Cluster_NAME --region REGION
```
Replace CLUSTER_NAME and REGION with the actual one.

### Complete output when script is complete run.
![image](https://github.com/user-attachments/assets/7acb0c51-2e10-476d-a4a7-509acb5194e2)  
![image](https://github.com/user-attachments/assets/d437b867-c859-4005-a00a-8c5f9d464b74)  






