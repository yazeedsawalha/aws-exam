# ECS Connection

We can connect to our EC2 instances using SSH or EC2 Instance Connect.


## What is EC2 Instance Connect?

EC2 Instance Connect is a simpler and more secure way to connect to your EC2 instances by web browser.


## What is SSH?
SSH is a protocol that allows you to securely access and manage your EC2 instances from a remote location.


- **Secure Shell (SSH)**:  
  - **Protocol**: TCP port 22.  

- **SSH Client**:  
  - **Linux/MacOS**: `ssh` command.  
  - **Windows**: `PuTTY`, `Xshell`, `MobaXterm`.  

- **SSH Command**:  
```
ssh -i /path/to/key.pem ec2-user@ec2-public-ip
```

- **EC2 User**:  
  - **Linux**: `ec2-user`, `ubuntu`, `centos`.  
  - **Windows**: `Administrator`.  

## SSH Key Pair

- **Key Pair**:  
  - **Public Key**: `id_rsa.pub`.  
  - **Private Key**: `id_rsa`.  

- **Key Pair Location**:  
  - **Linux**: `/home/ec2-user/.ssh/id_rsa.pub`.  
  - **Windows**: `C:\Users\Administrator\.ssh\id_rsa.pub`.  

- **Key Pair Creation**:  
  - **AWS Console**:  
    - Navigate to EC2 Dashboard.  
    - Click on "Key Pairs" in the left sidebar.  
    - Click on "Create Key Pair".  
    - Enter a name for the key pair.  
    - Click on "Create Key Pair".  
  - **AWS CLI**:  
       - `aws ec2 create-key-pair --key-name my-key-pair`.  
  - **AWS CLI**:  
    - `aws ec2 create-key-pair --key-name my-key-pair`.  

## SSH into EC2 Instance

- **SSH Command**:  
```
ssh -i /path/to/key.pem ec2-user@ec2-public-ip
``` 


## Example command in EC2

### 1 Update the package manager   
```
sudo yum update -y
```

### 2 Install Apache
```
sudo yum install -y httpd
```

### 3 IAM LIST users 
```
aws iam list-users
```


