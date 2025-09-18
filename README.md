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
<img> pic of wireshark website and homepage
</p>
<p>
First activity we want to do with this tutorial is to install wireshark from Wireshark.org, this application is used so the users may observe the triaffic the computer is both recieving as well as sending. After installing Wireshark and opening the program, the home page will show us the network interface card the device is using, we will highlight that by cliking on it then clicking on the shark fin to start monitoring the network traffic on the device
</p>
<br />

<p>
<img> pic of unfiltered data and pic of ICMP filtered data
</p>
<p>
when wireshark is initated, you will see the device is both sending and reeving lots of data, that is because even without interacing on the devices it is constantly having network activity. to see the specific trafic we want to see in this exersize we will use the filter section at the top of the window. The first protocall we want to observw is Internet Connection Media Protocl(ICMP), we wil type ICMP into the filter bar. IMCP is used when you want to ping a ip adress, ping is used to test the connection between two devices over the network. in the example above we ping a secondary VM, in wireshark we see the ping request and recived packets from the Vm we are using and from the secondary VM
</p>
<br />

<p>
<img azure NSGs settingss and constant pings before and after network change/>
</p>
<p>
in this next activity we will see what happens when we change the NSGs on the secondary to reject all incoming ping requests. First we will set up a constant ping command in our primary VM to ping the other VM endlessly, as before we get the same request nd recieved packets as before. We will then go into azure VM network settings and change it so that it wont accpect any inbound traffic, to do this we will log into azure, got to our desired VM and open its network settings, in those setting we will go to the NSG settings and set it to reject all traffic and move this setting up in priority. after that is saved we will go backn to our vm and observe the difference in trafffc data. In wireshark we see that all the oing requests timeot because the NSG on the secondary VM isnt sending a ping back, the NSG works somewhat like a firewall in this sense

  <p>
    img command line with commaand <ssh "username@<private ip> and wireshark packet recording of ssh data
  </p>
  <P>
in this next activity we are going to observe the triffic recorded when using the SSH command to remotely connect to the secondry VM using the command line. first step is to put the "ssh" filter in the section of wireshark. next we will open the command line and input the command <ssh labuser@10.0.0.4>, labuser is the username one the secondary VM and 10.0.0.4 is the private ip address of the VM, type yes for the question to continue with you connections, next it will ask for the password. after connecting the command line will dispaly the username and IP of the vm we connected to, on wireshark there will be traffic that was used to established the connections. notice as well that any keystroke in the command line will create trafffic, tis is because the command line is directing controling the device and that data is sent over the network. also note thhat if you dive into the data captured with wireshark, you will see its all encrypted, all data sent using SSH is designed this way
  </P>

  <p>
img command line with ipconfig /renew and wireshark showing triaffic captureed
    
  </p>

  <p>
    in this next activity we will observe traffic involved with DHCP. in wireshark's filter bar we will put the filter DCHP, open command line as admin and we will run a command to ask for a new IP address. in command line we will run the command "ipconfig /renew" this will make the device brodast a signal to request a new IP andress. the DNS will see this signal and acknolage that request, but since the device already has an IP address, the interaction ends there instead of the typical full interation when a device needs their first IP address, you can get the full paket traffic if you use the command /releaase but when using a remote desktop connection, it severs the connetion.
  </p>

  <p>
    img wireshark traffic after ussing nslookup, command console with the nslookup results
  </p>

  <p>
    Activity 4 - Obsevering DNS Traffic, in this ativity we will observe trafiic involved with DNS, Domain Naming System. the purpose of dns is to translate human readable website names into IP adresses. for this activity we will use the ommand line command "nslookup", with this command we can enter a website and get the IP address assosiated with it. First step is to enter the DNS filter in the filter bar on wireshark. in the pictures above we use nslookup to find the IP addresses of both disney.com and pixar.com, and in wireshark we can see all the traffic used to get that information   
  </p>

  <p>
    img wireshark capture of all the spam traffic
  </p>

  <p>
    Activity 5 - Remote Desktop Protocal (RDP)
    in this activity we will observe all the traffic involving the RDP. RDP is the protocol used when establishing a remote connection between two devices. In wireshark, we will enter "tcp.port == 3389", this is the network port RDP uses to establish a connection
  </p>
<br />
