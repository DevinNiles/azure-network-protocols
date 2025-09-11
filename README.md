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
- Activity 4
- Activity 5

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
when wireshark is initated, you will see the device is both sending and reeving lots of data, that is because even without interacing on the devices it is constantly having network activity. to see the specific trafic we want to see in this exersize we will use the filter section at the top of the window. The first protocall we want to observw is Internet Connection Media Protocl(ICMP), we wil type ICMP into the filter bar. IMCP is used when you want to ping a ip adress,
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
