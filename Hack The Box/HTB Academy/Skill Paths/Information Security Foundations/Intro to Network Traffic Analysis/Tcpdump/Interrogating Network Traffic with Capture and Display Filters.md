- This lab aims to provide some exposure to interrogating network traffic and give everyone some valuable practice implementing packet filters. We will be utilizing filters like `host`, `port`, `protocol`, and more to change our view while digging through a .PCAP file.
- Now that we have proven capable of capturing network traffic for the Corporation, management has tasked us with performing a quick analysis of the traffic our team has captured while surveying the network. The goal is to determine what servers are answering DNS and HTTP/S requests in our local network.
- If you wish to take a more exploratory approach to this lab, I have posted the overall tasks to accomplish. For a more detailed walkthrough of how to complete each step, look below each task in the solution bubble.


## Tasks
- Utilizing `TCPDump-lab-2.zip` in the optional resources, perform the lab to the best of your ability. Finding everything on the first shot is not the goal. Our understanding of the concepts is our primary concern. As we perform these actions repeatedly, it will get easier.



#### Task #1
- `Read a capture from a file without filters implemented.`
- To start, let's examine this pcap with no filters applied.

```shell-session
secmancer@htb[/htb]$ tcpdump -r (file.pcap)
```




#### Task #2
- `Identify the type of traffic seen.`
- Take note of what types of traffic can be seen. (Ports utilized, protocols, any other information you deem relevant.) What filters can we use to make this task easier?
- What type of traffic do we see?
- Common protocols: We should notice a bunch of `DNS, HTTP, and HTTPS` traffic.
- Ports utilized: `53 80 443`


#### Task #3
- `Identify conversations.`
- We have examined the basics of this traffic, now determine if you notice any patterns with the traffic.  
- Are you noticing any common connections between a server and host? If so, who?
	- What are the client and server port numbers used in the first full TCP three-way handshake?
	- Who are the servers in these conversations? How do we know?
	- Who are the receiving hosts?
- To help make this more straightforward, turning absolute sequence numbers on `(-S)` will be extremely helpful in determining conversations.
- We can also examine the different hosts involved. Servers typically communicate over the well-known port number assigned to the protocol `(80 for HTTP, 443 for HTTPS, for example)`. Hosts or recipients in the conversations will typically utilize a random high port number.



#### Task #4
- `Interpret the capture in depth.`
- Now that we have some familiarity with the pcap file, let's do some analysis. Utilize whatever syntax necessary to accomplish answering the questions below.
	- What is the timestamp of the first established conversation in the pcap file?
	- What is the IP address/s of apache.org from the DNS server responses?
	- What protocol is being utilized in that first conversation? (name/#)
- To determine the correct timestamp: Read the file with (-r) and then examine the conversations. Find the first one established ( Full TCP Handshake "Syn / SYN-ACK / ACK") and look at the first field in the output to find the timestamp. To find the IP of Host ( ), we can filter the traffic only to see conversations Sourcing from it ( src 'name-of-host' ) and then disable Name resolution with (-n). To determine the protocol being utilized in the first conversation, look for the well-known port # while disabling hostname and port name resolution (-nn) or leave off the (-nn), and it will tell you the name of the protocol in the output.



#### Task #5
- `Filter out traffic.`
- It's time to clear some of this data out now. Reload the pcap file and filter out all traffic that is not DNS. What can you see?
- Who is the DNS server for this segment?
- What domain name/s were requested in the pcap file?
- What type of DNS Records could be seen?
- To clear out everything that is not DNS, we can utilize:

```shell-session
secmancer@htb[/htb]$ sudo tcpdump -r (file.pcap) udp and port 53    
```

- Keep in mind that DNS is a protocol that utilizes both UDP and TCP for different functions. This means we may have to filter for both to ensure we don't miss anything.
- If the -X switch is utilized, we can get a Hex and ASCII output to look at cleartext names in the output.
- Understanding the DNS protocol requests and responses will help determine what type of records are being requested. The protocol-specific information field will often hold our answer.
- Now that we are only seeing DNS traffic and have a better grasp on how the packet appears, try to answer the following questions regarding name resolution in the enterprise: Who requests an A record for apache.org? (hostname or IP)
- What information does an A record provide?
- Who is the responding DNS server in the pcap? (hostname or IP)




#### Task #6
- `Filter for TCP traffic.`
- Now that we have a clear idea of our DNS server let's look for any webservers present. Filter out the view so that we only see the traffic pertaining to HTTP or HTTPS. What web pages were requested?
- What are the most common HTTP request methods from this PCAP?
- What is the most common HTTP response from this PCAP?
- **Filtering on port 80 OR 443 is a great start. You can also filter on the protocol name HTTP OR HTTPS. Keep in mind that ports are more like guidelines. I can host a webserver on any open port that can be bound. (8080 or 8001, for example)


#### Task #7
- `What can you determine about the server in the first conversation.`
- Let's take a closer look. What can be determined about the webserver in the first conversation? Does anything stick out? For some clarity, make sure our view includes the Hex and ASCII output for the pcap.
- Can we determine what application is running the webserver?
- Often the webserver will include pertinent information in the post responses such as OS or web server name. You may also be able to determine what service is running the webserver based on these responses. This task is a bit difficult to perform utilizing tcpdump. It requires us to look at the ASCII of the HTTP responses. In future sections, when we move into Wireshark, this will be much easier to do.


## Summary
- Through this lab, we expanded our horizons while utilizing TCPDump to analyze PCAP traffic. We learned how to capture and display filters effectively, dissected traffic to determine what protocols were running in the environment, and even gleaned some critical information about our enterprise segments, DNS, and Webservers. Continue to play on your own and see how deep the rabbit hole goes. Can you capture traffic in your home network and answer the same questions?



## Tips For Analysis
- Below is a list of questions we can ask ourselves during the analysis process to keep on track.

|  |
| --- |
| what type of traffic do you see? (protocol, port, etc.) |
| Is there more than one conversation? (how many?) |
| How many unique hosts? |
| What is the timestamp of the first conversation in the pcap (tcp traffic) |
| What traffic can I filter out to clean up my view? |
| Who are the servers in the PCAP? (answering on well-known ports, 53, 80, etc.) |
| What records were requested or methods used? (GET, POST, DNS A records, etc.) |

## Questions
- What are the client and server port numbers used in first full TCP three-way handshake? (low number first then high number)
	- 80 43806
- Based on the traffic seen in the pcap file, who is the DNS server in this network segment? (ip address)
	- 172.16.146.1