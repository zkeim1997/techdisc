---
title: "Certificates"
date: 2019-02-04
categories:
- category
- subcategory
tags:
- Certs
- x.509
keywords:
- tech
thumbnailImage: /img/cert.png
thumbnailImagePosition: left
---

<!--more-->
### Purpose
In this tutorial I will be exploring the use of certificates and how they can be used in an enterprise environment. To start this tutorial it is helpful to understand what a PKI (public key infrastructure) is. A PKI is a system that allows for distribution, verification, and revocation of public keys that can be used to transfer sensitive over the internet. Asymmetric encryption is what enables all of this. The whole premise behind this idea is that a client can use a **public key** to encrypt a challenge message. The only way to decrypt this message is to do so with the **private key**, which only the owner has. After verification the client and host are able to transfer a symmetric key securely and use this symmetric key for data transfer. The symmetric key is used since it is much more efficient to use this method of encryption. Although that is not exactly how clients and hosts interact, it is the basic idea. Certificates are then used to verify that this host or server are who they say they are. It is a way of trusting them. In this tutorial I will be setting up __Certificate Authority__ in a private domain and then will be creating certificates for various https services. 

### Setting up the Certificate Authority

For this tutorial Windows Server 2016 was used as our Certificate Authority. Below were steps to install Active Directory Certificate Services. 

1. In Server Manager, navigated to **Add Roles and Features**
2. Selected **Role-Based or feature-based installation**
3. Selected the local computer for **Destination server**
4. Clicked **Next** until the **Install** button
5. After installation selected **Configure Active Directory Certificate Services on the destination server**
6. Select **Certification Authority** in Role Services
7. Next verified that Enterprise CA is selected and clicked **Next**
8. Selected **Root CA** for the type of CA
9. Selected **Create a new private key** for the __Specify the type of private key__
10. For the Cryptography the default settings were kept
11. Selected Desired CA Name
12. Selected Desired Validity period
13. Lastly clicked **Configure** on the Confirmation page


### Native Trust Set-Up

Next a GPO was created so that all domain computers would natively trust our newly created CA. This is so that internal websites could be setup with SSL and would be trusted. Below were the steps.

1. In a web browser, navigated to “localhost/certsrv” and clicked Download a CA Certificate
2. Clicked Install this CA certificate to download the certificate “certnew.cer”
3. In the ‘Downloads’ folder, opened “certnew.cer” and clicked Install Certificate...
   - Selected “Local Computer” | **Next**  
   - Selected “Place all certificates in the following store” | **Browse**  
     - Selected “Trusted Root Certificate Authorities” | **OK** | **Next** | **Finish**  
4. Opened Windows PowerShell as administrator and executed mmc command to open Microsoft Management Console
   - Clicked the “File” tab and selected Add or Remove Snap-ins  
     - Selected “Group Policy Management” | **Add** | **OK**  
   - In the left column, navigated Group Policy Management > Domains > SRV2012.lcl or SRV2016.lcl   
   - Right-clicked Default Domain Policy and selected **Edit**  
     - In the Group Policy Management Editor, navigated Default Domain Policy > Computer Configuration > Policies > Windows Settings > Security Settings > Public Key Policies | **Next** | **Browse**  
     -Right-clicked “Trusted Root Certification Authorities” and selected **Import**  
     - Opened “certnew.cer” from the downloads | **Next** | **Next** | **Finish**  
     - Opened Certificate Services Client - Auto-Enrollment  
     - Set “Configuration Model” to **Enabled**  
     - Set both checkboxes to true | **Ok**  
   - Right-clicked Default Domain Policy and selected **Enforce**  
5. In Windows Powershell, executed gpupdate /force command to update group policy  



### Setting Up SSL for Web Server

Next we'll be using the newly created Certificate Authority to sign a certificate for an Apache web server running on a CentOS box. After completing these steps the website will now utilize encryption and because all clients in the domain trust the created CA, there will be no warning messages. Below are the steps. Commands are bolded.

1. On CentOS server, apache was started  
   - **sudo systemctl start httpd**  
2. Checked that Apache was up, shown in Figure x.
   - **sudo systemctl status httpd**
3. Host Firewall was opened
   - **firewall-cmd --zone=public --permanent --add-service=http**
   - **firewall-cmd --zone=public --permanent --add-service=https**
   - **firewall-cmd --reload**
4. The SSL Module was enabled
   - **sudo yum install mod_ssl**
   - **sudo systemctl restart httpd**
5. The Certificate Request was generated
   - **cd /etc/httpd/conf**
   - **openssl req -new -newkey rsa:2048 -nodes -keyout website.key -out website.csr**
6. The Request was exported from CentOS to the Windows Server
   - Note: WinSCP is a tool to enable SSH on Windows Machines and was installed at this address - https://winscp.net/eng/download.php
     - WinSCP was started
     - At the login menu it was connected to our web server using correct SSH credential and IP address
     - Selected login 
     - Navigated to /etc/httpd/conf on CentOS
     - Opened and copied Certificate Request
7. The Certificate Request was signed
   - http://localhost/certsrv was navigated to
   - **Request a certificate** task was selected
   - **advanced certificate request** was selected 
   - **Submit a certificate request** was selected
   - The Certificate Request was pasted into first text box
   - The Certificate Template was changed to Web Server
   - **Submit** was selected
   - The Base 64 encoded certificate was installed and saved
   - The cert was renamed: website.cer
8. The Signed Certificate was exported to Web Server using WinSCP
9. The key and certificate were moved to the appropriate directory
   - **mv website.key /etc/pki/tls/private/ca.key**
   - **mv website.cer /etc/pki/tls/certs/ca.crt**
10. The SSL Configuration was edited on CentOS
   - __sudo vim /etc/httpd.conf/ssl.conf__
   - SSLCertificateFile was changed to: __/etc/pki/tls/cert/ca.crt__
   - SSLCertificateKeyFile was changed to: __/etc/pki/tls/private/ca.key__
   - __:wq__
11. Apache was restarted
12. __sudo systemctl restart httpd__
13. https://CentOS_Ip_Address was navigated to from the Windows Server to verify


In conclusion, through this project I gained a better understanding of the purpose of certificates and how they can be used in an enterprise environment. Although these are not best practice methods for distributing certificates and generating certificate requests it is a good lab for simulation. 

