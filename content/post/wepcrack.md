---
title: "Cracking WEP"
date: 2019-02-02
categories:
- WLAN Security
tags:
- WLAN Security
- WEP
keywords:
- WLAN
thumbnailImage: https://techdisc.netlify.com/img/air.jpg
thumbnailImagePosition: left
---

<!--more-->

WEP is a WLAN protocol that was created as a way to encrypt traffic flowing from the client to an access point wirelessly. By doing this it prevented attackers from being able to capture packets and eavesdrop on victims. Unfortunately because of fundamental weaknesses in the RC4 cipher stream, WEP has been cracked and I will be showing a tutorial on how to do this using aircrack-ng. Packets are encrypted with WEP using an RC4 cipher stream using a 64 bit RC4 key. This key is made up of a 40 bit WEP key and a 24 bit IV. When a client wishes to connect to the access point they must enter this 40 bit WEP key. The IV is then used in conjunction with the WEP key during encryption to add randomness and to ensure each packet is encrypted with a different encryption key. RC4 engine will generate a cipher stream that is then XORed against the plaintext. The encrypted packet is sent with the IV in clear text. 

### Why is it Insecure
One fundamental issue with WEP is that there is no key management system. Because of this WEP keys rarely change because of how time consuming it is. It would take a bit of time to type a new 40 bit WEP key in 30 workstations for instance. The WEP key should be changed frequently but all an attacker needs is this key to gain full access to the network. Another major issue with WEP is that the IV is too small (24 bits). If an attacker can find a reused IV, this will allow them to decrypt or forge packets. There are only 16 million IV values so it only take a matter of time until an IV is used twice. The IV is also sent in clear text meaning that if an attacker can obtain two encrypted packets with the same IV, the original XOR of the packets can be found by XORING the encrypted packets again. 

### What’s needed for this tutorial
* An Access Point that uses WEP “open authentication”  
* A NIC capable of injecting packets  
* Aircrack-ng   

### My Setup
* MAC address of Wireless USB Adapter: 00:26:f2:b9:09:f1  
* Operating System: Ubuntu 18.04 (bionic)  
* Access Point: Ubiquiti AC Pro  
* Access Point MAC Address: 82:2A:A8:81:2F:44  
* WEP Key: zzzzz  

### Step 1: Starting Interface in monitor mode

You can start the Wireless nic by using the **airmon-ng** command shown below. Ifconfig was used to determine the interface name shown below. The 4 at the end of the command specifies the channel that the AP is being broadcasted on.

<img src="https://techdisc.netlify.com/img/startnic.png">

### Step 2: Fake Authentication with Access Point

Aireplay-ng can be used as shown below to associate to the access point. The __-1__ indicates the “fake authentication”. The __0__ indicates 0 reassociation timing in seconds. The __-e__ flag is the ESSID of the WEP network. The __-a__ flag is the BSSID of the access point and the __-h__ is the MAC address of the attacker interface. Lastly wlan0mon is the interface name.

<img src="https://techdisc.netlify.com/img/fakeauth.png">

### Step 3: Obtain PRGA

Next we will use the chopchop attack to acquire a pseudo random generation algorithm file that will then be used to forge new packets. Shown below we will use airplay-ng again. This time __-4__ is used for the chopchop attack. The __-h__ flag will stay the same and the __-b__ flag is now the BSSID of the access point. The system will respond when it finds a packet from the access point and will ask if you would like to use it shown below. You can then enter __y__ to continue. It will then calculate the offsets. 

<img src="https://techdisc.netlify.com/img/chopchop.png">

Once the program is successful you will see the output shown below and can move on to the next step.

<img src="https://techdisc.netlify.com/img/chopchopsuc.png">

Note: The attack most likely won’t be successful the first time. It is normal to have to run it multiple times. 

### Step 4: Forge an ARP Packet
Now we can use the xor file in the previous step to generate a packet for injection. When we inject this packet the access point will rebroadcast the arp packet and we can obtain new IVs which will be used to crack the WEP key. The following command will be used:  
__sudo packetforge-ng -0 -a 82:2A:A8:81:2F:44 -h 00:26:f2:b9:09:f1 -k 255.255.255.255 -l 255.255.255.255 -y replay_dec-0211-153926.xor -w arp-request__

You will want to replace the __-y__ flag object with your own .xor file created previously as well as your MAC (-h) and the AP MAC (-a). 


### Step 5: Capture generated IVs
Now we will use airodump-ng to start capturing generated IVs. Below the command with output is shown. __You will want to run this command in its own terminal window.__ Keep this running.

__Command:__ sudo airodump-ng -c 4 --bssid 82:2A:A8:81:2F:44 -w capture wlan0mon

<img src="https://techdisc.netlify.com/img/airodump.png">

### Step 6: Inject the ARP Packet
Now let’s inject the ARP packet so that  the AP will rebroadcast. Shown below is the command and output. Run this command as well in its own window. It will respond and ask to use a packet. You will want to enter __y__ to continue. 

<img src="https://techdisc.netlify.com/img/inject.png">

### Step 7: Obtain WEP key

Lastly we will open another terminal window and use aircrack-ng to crack the WEP key. Shown below is the command and the output. 

<img src="https://techdisc.netlify.com/img/crack.png">

### Conclusion
The key was found to be zzzzz in ASCII. As said before the WEP key used is 40 bits. In ASCII each letter is equal to 8 bits. Although this attack worked there are other precautions an attacker could take like spoofing another clients MAC address. Also a last note that this attack is useful since it doesn’t require any clients to be connected since we essentially create our own traffic. There are still many WEP networks that are in use and can even be found in hospitals. Because of the huge security holes these networks should be upgraded if possible.  


### Sources

https://www.aircrack-ng.org/
http://www.opus1.com/www/whitepapers/whatswrongwithwep.pdf


