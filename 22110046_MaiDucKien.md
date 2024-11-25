# Lab #2,22110046, Mai Duc Kien, INSE330380E_01FIE
# Task 1: Transfer files between computers  
**Question 1**: 
Conduct transfering a single plaintext file between 2 computers, 
Using openssl to implementing measures manually to ensure file integerity and authenticity at sending side, 
then veryfing at receiving side. 

**Answer 1**:

# Prepare client kien and linh
![image](https://github.com/user-attachments/assets/39b41169-5293-44f5-aa7c-93e4aea762f8)
![image](https://github.com/user-attachments/assets/0b2ec286-1d65-45c9-a163-acdec416f446)

Kien have ip ***10.111.5.186*** <br>
Linh have ip ***10.111.5.171*** <br>

setup ssh
```
sudo apt update
sudo apt install openssh-server
```
start ssh
```
sudo systemctl start ssh
```
status ssh
```
sudo systemctl status ssh
```
![image](https://github.com/user-attachments/assets/aaa717ed-6bfc-4e4c-a04f-8c3e344e0997)
![image](https://github.com/user-attachments/assets/1e64fe1a-3e40-4416-9fd2-d0ea29e6bc22)

# Create File in kien computer
![image](https://github.com/user-attachments/assets/ec7aee59-acff-4b26-a442-bdc8ab345b8b)
Open file
![image](https://github.com/user-attachments/assets/2365bcf1-7198-457e-a10d-7ffb2e98bc84)

# Ping 2 computer
![image](https://github.com/user-attachments/assets/6412e622-89b3-4934-b2ed-0e05ae5a268f)

![image](https://github.com/user-attachments/assets/465f12d0-dd69-496f-b308-2201b221daa3)








 
# Task 2: Transfering encrypted file and decrypt it with hybrid encryption. 
**Question 1**:
Conduct transfering a file (deliberately choosen by you) between 2 computers. 
The file is symmetrically encrypted/decrypted by exchanging secret key which is encrypted using RSA. 
All steps are made manually with openssl at the terminal of each computer.

**Answer 1**:


# Task 3: Firewall configuration
**Question 1**:
From VMs of previous tasks, install iptables and configure one of the 2 VMs as a web and ssh server. Demonstrate your ability to block/unblock http, icmp, ssh requests on the other host.
