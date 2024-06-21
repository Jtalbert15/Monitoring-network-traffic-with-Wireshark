# Monitoring-network-traffic-with-Wireshark

<img width="186" alt="Screenshot 2024-06-20 at 10 32 35 AM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/b36ae259-a6df-431b-89fc-1300d244ae81">

<h1>Summary</h1>

In this lab we will use Wireshark to monitor our network. WireShark will capture network activity and allow us to inspect many aspects of the data sent. We will be using filters to narrow down the data we want to view. We will view different TCP and UDP connections and explain what they do.

<h1>Things to know</h1>

Chances are your network is very busy and Wireshark is going to feed you a lot of information fast. Understanding these concepts will help you understand the information Wireshark is providing.

<h1>Ports</h1>

Your computer has port numbers ranging from 0 to 65,535. They are not physical ports but rather a way for a computer to decide which data goes where. For instance a HTTPS request would use TCP port 443. TCP is one of the 2 main types of ports with the other being UDP.

<h1>TCP vs UDP</h1>

TCP (Transmission Control Protocol) is a connection based protocol. Meaning there needs to be an established connection for data to be transmitted. This is done via a "3 way handshake". UDP (User Datagram Protocol) is not connection based so if data is not received back then the request must be sent again.


<h1>Data encapsulation</h1>

<img width="591" alt="Screenshot 2024-06-20 at 8 36 35 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/2ec92b19-b2ed-4182-97e6-2a6e1c04d583">

<h3>Ethernet</h3>

At the ethernet level we determine the destination and source address by the MAC address. Each device has its own unique MAC address.

<h3>IPV4</h3>

At this stage we determine our source and destination address by IP addresses. We also have many other pieces to our header. We have a TTL (Time to Live) that makes sure our data isn't floating around the internet endlessly. We also have a checksum that checks to make sure all data is present.

<h3>TCP</h3>

At this level we have a source and destination port. We also have a checksum to make sure all data is present. We also have a sequence number that allows us to rearrange our data if for instance data packet 4 arrives before data packet 3.

<h1>Step 1) Monitoring the network</h1>

To start after installing Wireshark open the application.

<img width="1003" alt="Screenshot 2024-06-20 at 2 50 55 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/87d341e7-1aa9-4437-bc0c-578a96854ce7">

You can see we have many selections to choose from but since my laptop is running on wifi I will select Wi-Fi: en0.

<img width="991" alt="Screenshot 2024-06-20 at 3 02 10 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/baf073ab-4fbf-422f-84d9-b2eda4845be9">

Now Wireshark is monitoring the network and logging the information for us.

<img width="797" alt="Screenshot 2024-06-20 at 3 12 37 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/4e170160-1d4c-44dc-b732-80d6e2b04ffd">

We can stop the monitoring of data by clicking the red square at the top of the screen.

We can also start a new monitoring session by clicking the blue shark fin to the left of the red square.


<h1>Step 2) ARP</h1>

ARP (Address Resolution Protocol) allows our router to figure out where to send information. Each device has its own MAC (Media Access Control) address. In order for our router to know where to send information it needs to know which device requested the information. An ARP request allows our router to figure out which IP address is associated with what device.

Let's take a look at what an ARP request looks like. Just under the blue shark fin we can filter our data. For an ARP request all we need to do is type arp followed by hitting enter.

<img width="1003" alt="Screenshot 2024-06-20 at 4 27 54 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/f9c4afd6-f59e-4b08-abde-56d13c630b6e">

In the right corner under the info section we can see that it is asking who is at different IP addresses and to tell the IP address at 192.168.1.254. On the sixth line we can see 192.168.1.250 is at 3c:22:fb:3f:b5:8f. This is telling the router that the device with the MAC address of 3c... has been assigned the IP address of 192.168.1.250.

<h1>Step 3) DNS</h1>

DNS (Domain Name Service) makes it easier for us to communicate with networks. Instead of having to remember the IP address we are trying to connect to we can type google.com and DNS will find the IP address we need.

Let's filter for DNS. Where we filtered for ARP we can now filter for DNS. Type DNS and hit enter

<img width="1007" alt="Screenshot 2024-06-20 at 4 59 39 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/af89dda8-4185-41d3-af94-707a312e095e">

We can see that DNS uses UDP port 53. We can tell whether the data is inbound or outbound based on the source port. We can see the queries are sent and responded to using the same port number that was assigned by the machine requesting information.

<h1>Step 4) HTTPS</h1>

HTTPS (Hypertext Transfer Protocol Secure) allows for safer web browsing. HTTPS uses TCP port 443 and provides encryption for our data. 

We can filter for HTTPS requests by typing tcp.port == 443 in the filter 

<img width="968" alt="Screenshot 2024-06-20 at 5 45 52 PM" src="https://github.com/Jtalbert15/Monitoring-network-traffic-with-Wireshark/assets/66844406/b8ef4d42-fe56-4b6c-af6a-c6e1f8bf337a">

We can see TCP requests as well as TLS (Transport Layer Security). TLS allows us to encrypt our data so that is more secure.
