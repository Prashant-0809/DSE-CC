# Terraform-work 

### Introduction
Terraform is a popular Infrastructure as Code (IaC) tool developed by HashiCorp, and it’s widely used for provisioning, managing, and automating infrastructure across various cloud providers
(e.g., AWS, Azure, Google Cloud) and on-premises environments.


## Installation  (Linux)

### 1. Update the System:
```
sudo apt update && sudo apt upgrade -y
```


![Screenshot 2025-03-23 093229](https://github.com/user-attachments/assets/730e5dbb-2f8d-41d1-be4d-c23f0c68d1d0)



### 2. Install Dependencies:
```
sudo apt install -y gnupg software-properties-common curl
```



![Screenshot 2025-03-23 093338](https://github.com/user-attachments/assets/58b99b82-ab4a-4817-aa4d-5044a84e8889)

### 3. Add the HashiCorp GPG Key:
```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```



### 4. Add the HashiCorp Repository:
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### 5. Install Terraform:
```
sudo apt update
sudo apt install terraform -y
```

![Screenshot 2025-03-23 093607](https://github.com/user-attachments/assets/75eec2d9-1e11-4b20-9de5-e14ac92e9472)

 Verify Terraform
```
terraform -version
```


------------------------------------------------------------------------------------------------------
## AWS CLI installation 
```
sudo snap install aws-cli --classic
```

-------------------------------------------------------------------------------------------------------

## AWS setup

### 1. IAM (Identify and Access management)
** Go to user groups in IAM, Create a User Group
** take Acces key from the user

-----------------------------------------------------------------------------------------------------------------------
## Configure AWS:
```
aws configure
```

Manually Adding AWS Credentials
```
aws_access_key_id = YOUR_ACCESS_KEY
aws_secret_access_key = YOUR_SECRET_KEY
region = us-east-1
```
Writing the Terraform Configuration File

```
mkdir terraform-ec2 && cd terraform-ec2

```
let's create a EC2 instance through code: - 
Create a file named ***main.tf***, and add the following configuration:

``` for example
provider "aws" {
    profile = "default"
    region  = "ap-south-1"
}

resource "aws_instance" "UGO_Server" {
    ami           = "ami-0cbf43fd299e3a464"
    instance_type = "t2.micro"

    tags = {
        Name = "MyNCAAInstance"
    }
}
```
use command 
```
nano main.tf
```

![Screenshot 2025-03-23 101935](https://github.com/user-attachments/assets/7af7d27e-0bd0-4cd5-95de-01b469ce03b3)

## Initializing and Applying Terraform

we need to initialize Terraform first !!
```
terraform init
```
![Screenshot 2025-03-23 101935](https://github.com/user-attachments/assets/cbba3a04-c194-4eff-9569-05daa683874e)

Check the Execution Plan
by Running
```
terraform plan
```

![Screenshot 2025-03-23 101949](https://github.com/user-attachments/assets/d71f49a3-108b-4e1b-8970-c68c866b30c5)

Deploy your EC2 instance:
```
terraform apply -auto-approve
```
![Screenshot 2025-03-23 103751](https://github.com/user-attachments/assets/ed0bd2e9-4e21-41ea-8b03-9fb8b8d78224)

![Screenshot 2025-03-23 103835](https://github.com/user-attachments/assets/7cc7d6f3-703c-4b10-a835-0c3df67f5815)

![Screenshot 2025-03-23 104021](https://github.com/user-attachments/assets/06ad9cb9-2d8e-44e7-a9de-416a17aa3533)

![Screenshot 2025-03-23 104038](https://github.com/user-attachments/assets/52845d02-45b7-48fe-809e-64f47a552d72)

