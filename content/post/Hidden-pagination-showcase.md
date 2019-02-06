---
title: "2017 Threat Landscape"
thumbnailImagePosition: left
thumbnailImage: https://techdisc.netlify.com/img/wannacry.png
date: 2018-02-15
categories:
- tranquilpeak
- features
tags:
- pagination
showPagination: false
---


<!--more-->

<h1>Threat Landscape</h1> 

This paper is intended to synthesize information contained in three sources that explain the cybersecurity threat landscape as of 2017. The information provided by these sources gives an idea of what attacks have been used previously, currently, and in the future. This paper will synthesize each journal individually.  

<h1>ISTR Financial Threats Review 2017</h1>

The first journal is ISTR’s Financial Threats Review of 2017 (Wueest, 2017). This journal provides research findings on cybersecurity attacks focused on corporations and financial institutes and gives an overview of popular attacks found in the wild. Although financial institutions have increased security measures, attacks on these companies can make millions of dollars. Attacks are carried out against their customers and the infrastructure of these institutions. Social engineering, credit card fraud, phishing, financial trojans, and mobile fraud are among the attack vectors used against customers. DDoS, blackmailing, bank2bank fraud, and ATM attacks as well as common attacks are used against the infrastructure (Wueest, 2017).  

More common in 2016 were attacks targeted at specific institutions. The journal explains a cyber heist conducted by a group called Lazarus against the Bangladesh central bank. This heist was extremely successful, and the group got away with 81 million US dollars (Wueest, 2017). The attackers gained access to the internal network and stole a bank operator’s credentials. Using these credentials, they made fraudulent transactions on the SWIFT network and used malware to cover their tracks. The group was caught after a typo was found creating suspicion. Carbanak group also conducted a similar attack where the institution was used to gain access to the SWIFT network to make fraudulent transactions. 

To distribute financial trojans spam email with malicious attachments are still heavily used. Office documents can also be used with malicious macros. Other attackers used social engineering and phishing attacks. Web exploit kits such as Angler, Neutrino, RIG, SundDown and Magnitude were also used through malvertising means. Tactics used consist of source code merging, sandbox evasion, remote desktop access, diversion, webinjects, redirection methods, session hijacking, fileless load points, overlay forms, atombombing injection and social engineering tactics (Wueest, 2017).  

In 2016 the most active threats against institutions were Ramnit, Bebloh, Snifula, and Zeus variants. Since 2015 there has been a 36% drop in detections however. This is attributed to security companies’ ability to block threats earlier in cyber kill chain (Wueest, 2017). Additionally, on average 38% of financial malware detections were from corporate computers (Wueest, 2017). Ramnit was the most used threat with Bebloh occupying second place.  

Japan had a large increase of malware detections making it the most attacked country globally with China in second, India in third, and the US in fourth. After analyzing 648 samples from four threat families it was found that the United States was the most targeted country counting by institutions. It was also found that Australia’s banks were the most attacked financial institutions. The United States was ranked first for most targeted mobile landscape. 

Although detections of financial malware continue to decrease, it is still a major issue. Targeting financial institutions is not easy but successful attacks pay out largely. The journal anticipates that this issue will remain a problem while attackers focus more heavily on corporate finance departments which seems very likely. This journal does a great job of citing throughout which makes it very credible. In many cases, however, they journal explains that they only used a few samples of the malware meaning that these statistics may not be completely accurate.  

<h1>ISTR Ransomware 2017</h1> 

ISTR’s Ransomware of 2017 explains ransomware and the recent self-propagating WannaCry and Petya (O’Brien, 2017). The journal explain that ransomware is now a key threat facing businesses particularly and can cause huge financial losses, disruption and reputational damage. During 2016, there was a dramatic increase in ransomware but has appeared to slow again. The U.S. is the region most affected by this malware accounting for 29% (O’Brien, 2017). The number of new ransomware variants has gone up with an increase around when WannaCry and Petya were discovered.  

WannaCry was not the first ransomware to use worm-like infection vectors. What made WannaCry so effective was the exploit it used call “EternalBlue.” This vulnerability was leaked by an organization called the Shadow Brokers and was created by the NSA. Once WannaCry appeared on a computer it would continue to use the EternalBlue exploit to infect other local computers and began to scan IP addresses to find other vulnerable computers in other networks (0’Brien, 2017). Symantec products were blocking this exploit around 80,000 times per hour. After registering a domain that the ransomware attempted to contact, a kill switch was discovered. The weeks following the attack evidence was found that could suggest that Lazarus may have been behind the attack.  

After WannaCry a similar attack called Petya was discovered to use the same EternalBlue exploit but also used other SMB network spreading techniques that allowed it to infect machines already patched against EternalBlue (O’Brien, 2017). Petya was much more targeted as well affecting mostly Ukraine. Petya was installed on a machine via a Trojanized version of MEDoc, an accounting software package. Once installed, Petya would create a list of IP addresses to infect. Petya also selected external IP addresses related to the organization instead of random ones like WannaCry. Petya would then build credentials and began spreading itself. It would not attempt to infect computers with Symantec products. It is argued that Petya was politically motivated against Ukraine given certain circumstances of targeting (O’Brien, 2017).    

Business organizations were found to be much more vulnerable to these types of attacks. The worm-like mechanisms used by WannaCry and Petya were able to spread across networks easily. Most home computer users will not be connected to networks and most home routers are able to block EternalBlue attacks. Consumers must be aware of other types of ransomware that do not rely on worm-like mechanisms. Most ransomware is delivered through spam campaigns and is sent to as many email addresses as possible. Targeted ransomware attacks can also be rewarding for attackers but requires great skill. First these attackers will gain a foothold, steal credentials, and conduct research using tools to learn which computers to infect and if they are any backups.  

Ransomware is a very costly threat to many organizations. If a company is infected it can be impossible to decrypt data without the key meaning you must pay the ransom. Besides the cost of paying the ransom, ransomware can also create disruption and can bring a whole company to a halt until the issue is resolved. This means loss of productivity and services that the company relies on to make a profit. The largest payout of ransom was by a South Korean web hosting company who payed 1 million dollars. According to research only 34% of victims will pay the ransom (O’Brien, 2017).  

Precautions should be taken to prevent this type of attack from occurring in the first place. Email security should be used to help filter and stop malicious emails before they even reach users. Intrusion prevention should be used to detect and block malicious traffic and prevent installation of ransomware. Browser protection should be used to block websites from exploitation. Users should also be educated on the dangers of ransomware and phishing attacks. If a computer is infected it is critical to contain the threat. Using an advanced antivirus engine, an infection can be detected very quickly. If a computer is infected it should be removed from the network and cleaned (O’Brien, 2017). 

If a company is affected by an attack there are many steps an organization can take to respond. First the primary infector must be identified to prevent further spreading. Analyzing the malware can give an idea of how the computer was infected and how the data was encrypted if a mistake was made. A data recovery provider can also help to recover some of the encrypted data depending on the sophistication of the malware.  

In many cases organizations need to take steps to ensure that they prevent this attack from occurring since it can be crippling. Organizations should adopt a multi-layered approach to ensure there are multiple defensive practices in place. This should include backups, regular patching, firewall implementations, gateway antivirus, intrusion detection systems, etc. (O’Brien, 2017.) The information used in this journal seems to be very credible. Sources and other studies used in the journal were cited. The journal did a great job of including recent ransomware attacks and the prices as well.  

<h1>DDoS attacks in Q2 2018</h1> 

This article begins by explaining some of the more major DDoS attacks that have occurred in quarter two. A botnet was created and formed from 50,000 surveillance cameras in Japan. A new type of malware has been created that is able to withstand a reboot. A hacker attacked Verge mining pools and was able to make $1.7 million (Ibragimov et.al, 2018).    

The article also explains that older or more forgotten vulnerabilities are being used, like CHARGEN. CHARGEN was created for testing and measurement. When listening in UDP mode, a server can respond to any request with a packet. Attackers use this protocol to send requests to a vulnerable CHARGEN server and then substitute the outgoing address with the victim. There still exist many CHARGEN servers on the internet (Ibragimov et.al, 2018). The authors explain that cybercriminals are looking at more retro methods of DDoS and are starting to target e-sport tournaments since they can be very profitable. DDoS attackers can also disrupt streaming services such as twitch.  

Mid-April was the worst period for DDoS attacks. China was number one in attacks with 59.03%. Attacks were spread out evenly among days of the week. SYN attacks rose to 80.2% and UDP attacks with 10.6%. Surprisingly Malaysia was fifth with 1.30% of all DDoS attacks. The longest attack during Q2 lasted almost 11 days. The share of attacks consisting of five to nine hours increased by almost 50%. Short-duration attacks fell to 69.49%. Concluding the article argues that the intensity of DDoS attacks is continuing to worsen (Ibragimov et.al, 2018). The most rewarding areas for DDoS attacks are currently cryptocurrencies and eventually will be e-sports tournaments. The data used in this article comes from Kaspersky Labs. Kaspersky labs monitors botnets using their DDoS intelligence system. This report provided these intelligence statistics for Q2 making it a reliable source for information.  

 

<h1>Conclusion</h1> 

The articles used for this paper covered topics about financial threats, ransomware threats, and DDoS threats. More importantly these resources used are current and give a good idea of the threat landscape our society faces online. The sources used do a great job of including most attacks that hackers are currently using. Furthermore, they explain what direction hackers are heading in terms of attacks and what to be prepared for. Most hackers in today’s age are either politically motivated or are following the money. Attacks against financial institutions and corporations using ransomware and DDoS attacks is where the money is currently and where hackers are most likely headed.   

 

<h1>References</h1>

Wueest, C. (2017). Financial threats review 2017. Internet Security Threat Report. 

O’Brien, D. (2017). Ransomware 2017. Internet Security Threat Report. 

Ibragimov, T., Kupreev, O., Badovskaya, E., Gutnikov, A. (2018). DDos attacks in q2 2018. 

 

 

 
