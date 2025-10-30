# Project 5: SSH Remote Server Setup

This project documents the successful setup and configuration of a remote Linux server (AWS EC2) to allow secure access using multiple SSH keys.

---

## Steps Taken to Complete the Project

### 1. Created AWS EC2 Instance
* **Action:** Launched a new `t2.micro` EC2 instance using the **Ubuntu 24.04 LTS** AMI.
* **Security:** Configured the security group to allow inbound SSH traffic (port 22) only from my IP address for enhanced security.

### 2. Created and Added First SSH Key
* **Action:** Generated a 4096-bit RSA key pair (`devops_key1` & `devops_key1.pub`) locally on my machine.
* **Integration:** Imported the public key (`devops_key1.pub`) into the AWS EC2 "Key Pairs" dashboard.
* **Login Test:** Successfully logged into the server using the command:
    `ssh -i ~/.ssh/devops_key1 ubuntu@<server-ip>`

### 3. Added a Second SSH Key Manually
* **Action:** Generated a second, independent key pair (`devops_key2` & `devops_key2.pub`) locally.
* **Configuration:** Logged into the server (using the first key) and manually added the contents of `devops_key2.pub` as a new line in the `~/.ssh/authorized_keys` file.
* **Login Test:** Successfully logged out and logged back in using the *second* key:
    `ssh -i ~/.ssh/devops_key2 ubuntu@<server-ip>`

### 4. Configured SSH Alias (`~/.ssh/config`)
* **Action:** Created and configured the `~/.ssh/config` file on my local machine.
* **Setup:** Added `Host` aliases (e.g., `aws-server`) that define the `HostName` (IP address), `User` (ubuntu), and `IdentityFile` (path to the private key).
* **Result:** I can now log in instantly using the simple command `ssh aws-server`.

### 5. (Bonus) Added an Elastic IP
* **Problem:** Noticed that the server's public IP changed after a stop/start cycle, breaking the alias.
* **Solution:** Allocated an **Elastic IP** from AWS and associated it with my EC2 instance.
* **Final Step:** Updated the `HostName` in my `~/.ssh/config` file to this permanent Elastic IP. My alias now works permanently.







