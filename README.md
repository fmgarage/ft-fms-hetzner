# fmserver-cloud

Run FileMaker Server 19 for Linux in the Hetzner Cloud.





## 1. Register an Account

Go to Hetzner and register a free account. If you [follow our referral link](https://hetzner.cloud/?ref=KzxqMaXk51C8), you get a € 20,– credit for your projects. In case you stay  with Hetzner, we receive a € 10,– bonus that we will donate to the [Stiftung Bildung](https://www.stiftungbildung.com). 



## 2. Add a Server

In the Console https://console.hetzner.cloud/projects create a project and in there add a new server. You will need Centos 7 and we strongly recommend adding the SSH key for you local machine. Start the server and ssh into it.



## 3. Installation 

We recommend downloading the installer from your Claris account, unzipping it and upload it to your web server. On the one hand downloads from Claris are sometimes very slow and on the other hand you can run the installer without having to download and unpack it first. As a good practice we also rename the rpm file and put it in a hard-to-guess folder.

`yum localinstall https://yourdomain.com/d0nf2tzu9e/fms-linux-installer.rpm -y`

This installs FileMaker Server interactively but you can also follow the instructions in the server's readme files for the assisted install. 

When complete, you restart the fmshelper and check, if your desired ports (5003, 16000 etc.) are listening:

`systemctl restart fmshelper`
`netstat -tulpn`

After that you should be good to go.



## 4. Optional Measures



#### Assign a floating IP

In the Hetzner Console you can 'install' an IP address that can be assigned to any server in your account. This can be used to configure a subdomain like **fmserver.yourdomain.com** and install an SSL certificate for your server.



#### Harden the Server

Yout server is now publically available and most likely under attack already. We recommend to close all the ports you do not need, [disable ICMP ping](https://www.thegeekstuff.com/2010/07/how-to-disable-ping-replies-in-linux/) and [move SHH to a non-standard port](https://blog.devolutions.net/2017/4/10-steps-to-secure-open-ssh).



#### Set up a VPN

You can install WireShark on the server: https://www.wireguard.com/install/ and close all public ports



https://support.claris.com/s/answerview?anum=000026067&language=en_US