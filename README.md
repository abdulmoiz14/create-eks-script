# EKS creation script guidelines
## First we need to install required pakages that we need for this script to run successfully.
### awscli version
#### check awscli version
```bash
aws --version```

#### if cli version is v1.x.x, than use below commands to upgrade the awscli to v2.x.x
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
sudo ln -s /usr/local/aws-cli/v2/current/bin/aws /usr/local/bin/aws
aws --version```


