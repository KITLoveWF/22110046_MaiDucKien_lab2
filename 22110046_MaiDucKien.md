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
```
echo "Day la file can gui tu may kien sang may linh" > file.txt
```
Open file
![image](https://github.com/user-attachments/assets/2365bcf1-7198-457e-a10d-7ffb2e98bc84)
```
cat file.txt
```

# Ping 2 computer
![image](https://github.com/user-attachments/assets/6412e622-89b3-4934-b2ed-0e05ae5a268f)

![image](https://github.com/user-attachments/assets/465f12d0-dd69-496f-b308-2201b221daa3)

# Transfering a single plaintext file between 2 computers
**1.Use scp to transfer files:**
```
openssl genrsa -out private_key.pem 2048
openssl rsa -in private_key.pem -pubout -out public_key.pem
```
![image](https://github.com/user-attachments/assets/df44847d-ff2f-48e6-8003-0d38b3e69b0a)

```
cat private_key.pem
```

![image](https://github.com/user-attachments/assets/591989d8-9a32-4183-9528-7f7d0082c333)
```
cat public_key.pem
```
![image](https://github.com/user-attachments/assets/e9377a92-d552-40a3-8967-a12a2c06be66)

**2. Calculate the hash of the file:**
Calculate the file's SHA256 hash to ensure integrity:
```
openssl dgst -sha256 -out file.txt.sha256 file.txt
```
**3. Create digital signature:**
Use private key to digitally sign files:
```
openssl dgst -sha256 -sign private_key.pem -out file.txt.sign file.txt
```
**4. Transfer files to Linh computer:**
Use scp to transfer files:
```
scp file.txt file.txt.sha256 file.txt.sign public_key.pem linh@10.111.5.171:/home/linh
```
**Result**
![image](https://github.com/user-attachments/assets/6341861c-4185-41ae-90cd-866a63ba4889)
**5.Verify**

```
openssl dgst -sha256 -verify public_key.pem -signature file.txt.sign file.txt
```
![image](https://github.com/user-attachments/assets/2b1d1faa-7f83-46ad-84ba-b200d52f9e8b)

```
cat file.txt
```

![image](https://github.com/user-attachments/assets/796edb5c-6284-4dba-81d1-92afe5bc232e)
















 
# Task 2: Transfering encrypted file and decrypt it with hybrid encryption. 
**Question 1**:
Conduct transfering a file (deliberately choosen by you) between 2 computers. 
The file is symmetrically encrypted/decrypted by exchanging secret key which is encrypted using RSA. 
All steps are made manually with openssl at the terminal of each computer.

**Answer 1**:
# Create File in kien computer
```
echo "Kien rat thich linh va mong linh cho kien 1 co hoi " > secret_file.txt
cat secret_file.txt
```


![image](https://github.com/user-attachments/assets/9904f0f1-66a2-4e53-8d7c-2482e767a505)
# Kien Client
**1 Encrypt file with secret key (AES)**
```
openssl rand -base64 32 > secret_key.bin
openssl enc -aes-256-cbc -salt -pbkdf2 -in secret_file.txt -out secret_file.enc -pass file:./secret_key.bin
```
**2 Encrypt secret key with RSA**
```
openssl rsautl -encrypt -inkey public_key.pem -pubin -in secret_key.bin -out secret_key.enc
```
**3. Send file**
```
scp secret_file.enc secret_key.enc private_key.pem linh@10.111.5.171:/home/linh
```
**Result**
![image](https://github.com/user-attachments/assets/a6df17c1-1671-4845-94c8-c6f2fb8dcb12)

# Linh Client 
**4**

![image](https://github.com/user-attachments/assets/8b5699b9-0c55-481d-a54a-1cd76a2c6dcd)





# Task 3: Firewall configuration
**Question 1**:
From VMs of previous tasks, install iptables and configure one of the 2 VMs as a web and ssh server. Demonstrate your ability to block/unblock http, icmp, ssh requests on the other host.
