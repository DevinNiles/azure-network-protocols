<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Tutorial Activities</h2>

- Activity 1 - install wire shark on VM
- Activity 2 - inpsect packet data and use ICMP filter
- Activity 3 - Network Security Groups(NSGs) effect on data traffic
- Activity 4 - DCHP filter and trafiic
- Activity 5 - DNS filter and traffic
- Activity 6 - RDP filter and traffic

<h2>Actions and Observations</h2>

<p>
<img> This picture shows the wireshark homepage where you can download the application <img width="2032" height="1062" alt="wireshark website" src="https://github.com/user-attachments/assets/c020cf1c-d09a-4454-803d-bdd653ed4a30" />
</p>

<p>
First activity we want to do with this tutorial is to install wireshark from Wireshark.org, this application is used so the users may observe the traffic the computer is both receiving as well as sending. After installing Wireshark and opening the program, the home page will show us the network interface card the device is using, we will highlight that by cliking on it then clicking on the shark fin to start monitoring the network traffic on the device
</p>
<br />

<p>
 This picture shows where the filter bar is in wireshark and the filter used in this excercise <img width="1452" height="304" alt="icmp in filter bar" src="https://github.com/user-attachments/assets/a22a1380-5a35-40eb-8608-629e430ee70a" />
</p>
<p>
 This picture shows the data being captured by wireshark without a filter in place
 <img width="2424" height="1162" alt="unfiltered wireshark data" src="https://github.com/user-attachments/assets/af467ffa-c12c-420c-902a-0121846a9eb9" /> 
</p>
<p>
 This picture shows the filtered ICMP data that occured from pinging the secondary VM
 <img width="2206" height="1392" alt="icmp ping demo" src="https://github.com/user-attachments/assets/ec6fd547-2660-41c9-b60c-9992bbe05a82" />
</p>

</p>
<p>
When wireshark is initated, you will see the device is both sending and receiving lots of data, that is because even without interacting on the device, it is constantly having network activity. To see the specific traffic we want to see in this exercise we will use the filter section at the top of the window. The first protocal we want to observe is Internet Control Message Protocl(ICMP), we will type ICMP into the filter bar. IMCP is used when you want to ping an ip address, ping is used to test the connection between two devices over the network. in the example above we ping a secondary VM, in wireshark we see the ping request and recived packets from the Vm we are using and from the secondary VM
</p>
<br />

<p>
 This picture shows the windows VM sending out constant ping requests to the linux VM
<img azure NSGs settingss and constant pings before and after network change/> 
</p>
<P>
<img width="944" height="436" alt="endless ping pre NSG" src="https://github.com/user-attachments/assets/5828c0fa-dfe3-4803-ab2a-969dd2572a93" />
</P>
<P>
<img width="1664" height="1358" alt="wireshark and console endless ping" src="https://github.com/user-attachments/assets/b33f834c-f41e-4fe4-86e6-fd5c40d42951" />
</P>

</p>
<p>
In this next activity we will see what happens when we change the Network Security Groups (NSGs) on the secondary VM to reject all incoming ping requests. NSGs are Azures Firewall so to speak. First we will set up a constant ping command in our primary VM to ping the other VM endlessly with the command "ping 10.0.0.5 -t", as before we get the same request and recieved packets. 
<img width="1342" height="1266" alt="VM linux network settings" src="https://github.com/user-attachments/assets/52df0f30-08be-4a48-9ff9-8cf455a3afa6" />
<img width="1606" height="1202" alt="azure NSG link" src="https://github.com/user-attachments/assets/ae08d127-cd72-49d0-a45f-391855f35367" />
<img width="1010" height="1096" alt="inbound security settings link" src="https://github.com/user-attachments/assets/cad5b68e-940c-4137-8bb6-ed2ac43a7841" />
<img width="1778" height="1282" alt="pre security rule page" src="https://github.com/user-attachments/assets/fc8d9ae8-03ac-44b0-80ad-56257fe7ba81" />

<img width="2060" height="890" alt="post-ICMP-rule" src="https://github.com/user-attachments/assets/f7cac307-da9c-4cc9-97a0-e14d30ae39d6" />

  We will then go into azure VM network settings and change it so that it wont accpect any inbound traffic, to do this we will log into azure, got to our desired VM and open its network settings, in those setting we will go to the NSG settings and click on "linux-VM-nsg", here we will click on ADD, tis will open an options window to create our new rule. the settings we want to change will be, "destination port ranges", we will change this to "*" as that represents any and ICMP doesnt use a port. we will also change "Protocol" to ICMPv4, the protocol ping uses. we will change "Action" to deny, to deny all incoming pings. and lastly we will change "Priority" to 290, this will set the new rule at the top of the list ensuring it is enacted first. 

<img width="1180" height="1010" alt="console page ping time outs" src="https://github.com/user-attachments/assets/cea8b6b9-14cb-493f-9d91-c80149ee9e5b" />

<img width="1900" height="770" alt="wireshark packets after ping denial" src="https://github.com/user-attachments/assets/fd3312db-c8db-49ab-8afb-64bf2950db00" />
after the rule has been added and we go back to wireshark and the command consile we can see that the ping requests are not going through and the requests are timing out instead, THats because the NSGs on the linux machine is blocking all data related to ICMP. the NSG works somewhat like a firewall in this sense

  <p>

<img width="1910" height="946" alt="wireshark ssh filtered" src="https://github.com/user-attachments/assets/949dbf54-bfe8-4b94-9579-4acefc26c39c" />

<img width="1744" height="972" alt="ssh connection to linux" src="https://github.com/user-attachments/assets/4f72911b-d9ae-4a62-b1f3-e84781612477" />


  </p>
  <P>
in this next activity we are going to observe the triffic recorded when using the SSH command to remotely connect to the secondry VM using the command line. first step is to put the "ssh" filter in the section of wireshark. next we will open the command line and input the command <ssh labuser@10.0.0.4>, labuser is the username one the secondary VM and 10.0.0.4 is the private ip address of the VM, type yes for the question to continue with you connections, next it will ask for the password. after connecting the command line will dispaly the username and IP of the vm we connected to, on wireshark there will be traffic that was used to established the connections. notice as well that any keystroke in the command line will create trafffic, tis is because the command line is directing controling the device and that data is sent over the network. also note thhat if you dive into the data captured with wireshark, you will see its all encrypted, all data sent using SSH is designed this way
  </P>

  <p>
img command line with ipconfig /renew and wireshark showing triaffic captureed

<img width="1210" height="904" alt="dhcp bat script command" src="https://github.com/user-attachments/assets/73bb8c4f-02ac-404a-8416-97803db94f72" />

<img width="522" height="202" alt="dhcp renew release script" src="https://github.com/user-attachments/assets/3a02120b-601d-42e1-9153-a4b7fab37acf" />

 <img width="1564" height="848" alt="dhcp wireshark activity" src="https://github.com/user-attachments/assets/52f0f3f5-2957-47f6-befb-30e49bb484dc" />

  </p>

  <p>
    in this next activity we will observe traffic involved with DHCP. in wireshark's filter bar we will put the filter DCHP, open command line as admin and we will run a command to ask for a new IP address. in command line we will run the command "ipconfig /renew" this will make the device brodast a signal to request a new IP andress. the DNS will see this signal and acknolage that request, but since the device already has an IP address, the interaction ends there instead of the typical full interation when a device needs their first IP address, you can get the full paket traffic if you use the command /releaase but when using a remote desktop connection, it severs the connetion.
  </p>

  <p>
    img wireshark traffic after ussing nslookup, command console with the nslookup results

   <img width="940" height="808" alt="nslookup" src="https://github.com/user-attachments/assets/1ddb75cc-1ec4-4df0-b2e7-0abf7ea4b7f5" />

<img width="2118" height="890" alt="dns traffic" src="https://github.com/user-attachments/assets/3bb79f79-e0cd-4686-878d-98eb5e9df303" />

  </p>

  <p>
    Activity 4 - Obsevering DNS Traffic, in this ativity we will observe trafiic involved with DNS, Domain Naming System. the purpose of dns is to translate human readable website names into IP adresses. for this activity we will use the ommand line command "nslookup", with this command we can enter a website and get the IP address assosiated with it. First step is to enter the DNS filter in the filter bar on wireshark. in the pictures above we use nslookup to find the IP addresses of both disney.com and pixar.com, and in wireshark we can see all the traffic used to get that information   
  </p>

  <p>
    img wireshark capture of all the spam traffic

   <img width="2100" height="922" alt="Screenshot 2025-10-14 211205" src="https://github.com/user-attachments/assets/ae803eca-3cd6-4332-818a-f76ef4b44ce7" />

  </p>

  <p>
    Activity 5 - Remote Desktop Protocal (RDP)
    in this activity we will observe the traffic involving the RDP. RDP is the protocol used when establishing a remote connection between two devices. In wireshark, we will enter "tcp.port == 3389" into the filter bar, this is the network port RDP uses to establish a connection. After starting the packet capture we can already see lots of network activity, this is beause we are already remotely connected to the VM and thats the data we are seeing. The RDP connection is onstantly streaming an image to our personal device so the traffic is frequent and constant. comparing SSH to RDP, SSH only sends network data when we interat with the connection between the devices, where as RDP is always sending data whether we are typing or not.
  </p>
<br />
