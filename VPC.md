# AWS VPC and EC2 Setup Guide

This guide provides step-by-step instructions for setting up a Virtual Private Cloud (VPC), launching an EC2 instance, and configuring Apache with SSL.

## Step 1: Create a VPC
1. Open the **AWS Management Console**.
2. Navigate to **VPC** > **Create VPC**.
3. Choose **VPC only** and specify:
   - **Name:** `MyVPC`
   - **IPv4 CIDR Block:** `10.0.0.0/16`
4. Leave other settings as default and click **Create VPC**.
   
![Screenshot 2025-03-21 122837](https://github.com/user-attachments/assets/50b85f76-d716-4cf7-97f2-ca1b39dfb3f5)

## Step 2: Create a Subnet
1. In the **VPC Console**, go to **Subnets** > **Create Subnet**.
2. Select the **VPC (MyVPC)**.
3. Choose an **Availability Zone**.
4. Enter **CIDR Block** (e.g., `10.0.1.0/24`).
5. Click **Create Subnet**.

![Screenshot 2025-03-21 122913](https://github.com/user-attachments/assets/f44b6f1b-07f5-4c4b-9740-4ff487a68dbd)


## Step 3: Create and Attach an Internet Gateway
1. Go to **Internet Gateways** > **Create Internet Gateway**.
2. Name it **MyIGW** and click **Create**.
3. Select **MyIGW**, click **Actions** > **Attach to VPC** > Select **MyVPC**.

![Screenshot 2025-03-21 123000](https://github.com/user-attachments/assets/617acdc5-12c9-4beb-8a15-d1fbb6a4fc98)
![Screenshot 2025-03-21 123058](https://github.com/user-attachments/assets/601f77ab-536e-4c0c-b957-ce03e917a91d)

## Step 4: Create a Route Table and Associate It with the Subnet
1. Go to **Route Tables** > **Create Route Table**.
2. Name it **MyRouteTable**, select **MyVPC**, and click **Create**.
3. Click on the **Routes** tab > **Edit Routes**.
4. Add a new route:
   - **Destination:** `0.0.0.0/0`
   - **Target:** Select **MyIGW**
5. Click **Save Routes**.
6. Go to **Subnet Associations** and associate **MySubnet** with **MyRouteTable**.

![Screenshot 2025-03-21 123037](https://github.com/user-attachments/assets/e84c2c6e-727d-4dfc-a7d1-f75dff7c6b94)

![Screenshot 2025-03-21 123116](https://github.com/user-attachments/assets/ff96fe78-8ab3-4d1c-a814-dcd7fa96914a)

## Resource map of vpc & security group

![Screenshot 2025-03-21 123239](https://github.com/user-attachments/assets/21b8fd14-6076-4356-af1b-bf1e2f1d5994)

![Screenshot 2025-03-21 123201](https://github.com/user-attachments/assets/a18c8c4f-f46a-4344-90cf-bad34f08224e)

## Step 5: Launch an EC2 Instance in the VPC
1. Navigate to **EC2** > **Launch Instance**.
2. Select **Amazon Linux** or **Ubuntu AMI**.
3. Choose an instance type (e.g., `t2.micro`).
4. In **Networking**, select:
   - **VPC:** `MyVPC`
   - **Subnet:** `MySubnet`
   - **Auto-assign Public IP:** `Enable`
5. Configure **key pair** and **security group** (allow SSH and HTTP).
6. Click **Launch**.

![Screenshot 2025-03-21 123359](https://github.com/user-attachments/assets/ac9498fb-e1a1-4ffc-8eea-e998d8e4e60f)

![Screenshot 2025-03-21 123434](https://github.com/user-attachments/assets/3155fd5b-6b39-461a-9dec-9ed0047999ad)

## Step 6: Install Apache and Download SSL Certificate
### SSH into Your EC2 Instance:
```bash
ssh -i my-key.pem ec2-user@<your-instance-public-ip>
```
### Install Apache2
```bash
sudo apt update && sudo apt install apache2 -y  # (For Ubuntu)
sudo systemctl start apache2
sudo systemctl enable apache2
````
### Download an SSL certificate
```bash
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
````
## Step 7: Create a Virtual Private Gateway (VGW) and Attach to VPC
1. In VPC Console, go to Virtual Private Gateways.
2. Click Create Virtual Private Gateway.
3. Name it (``MyVGW``) and Create.
4. Select ``MyVGW``, click Actions > Attach to VPC > Select ``MyVPC``.

![Screenshot 2025-03-21 123739](https://github.com/user-attachments/assets/0adda2c7-1559-4a26-b12a-625b09ec7dda)

## Step 8: Configure Routing for VGW
1. In Route Tables, go to MyRouteTable.
2. Add a route for on-premise/private networks (e.g., 192.168.1.0/24) pointing to MyVGW.
3. Click Save Routes.

![Screenshot 2025-03-21 123917](https://github.com/user-attachments/assets/55f609b9-c143-45c3-9aa6-373fb47b531a)

## Open the Public IP of Instance

![Screenshot 2025-03-04 235421](https://github.com/user-attachments/assets/2f394c3a-35df-415b-951a-fc86d2ddd17a)
