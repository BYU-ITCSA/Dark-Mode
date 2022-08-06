# How the Internet Works

Eric Pressler

---

## The OSI Model

I wouldn't get too bogged down here. The important points are:

1. any functionality can be replaced by itself and still operate with the rest of the stack (like how ethernet has replaced token ring or how IPv4 coexists with IPv6)
2. Headers are added and removed whenever you move to a lower or higher layer respectively
3. I'd only really go up to layer 3 here since most of the discussion would likely focus on layers 4-7.
4. even though we think of a router as a layer 3 device, it also operates on layers 2 and 1. After all, it has cables to connect it to other devices. It takes a packet, puts it in a frame, then transmitts raw bits across the medium.

a few notes:
Layer 1 is electrical (or optical) signals going through the air or down a wire or fiber optic cable.

Layer 2 is getting traffic to the correct device within the same VLAN/subnet. Don't worry about how those work, that's what Network Engineering Club is for.

Layer 3 is for getting traffic to the correct network. Once it is there, it hands it back down to layer 2 to get to the correct device.

Layer 4 is for your computer to recognize and differentiate the many concurrent connections it is using (when you send data, the recipient will swap the source and destination ports when replying, and the computer is listening on the port it sent from for that response). This is how you can use HTTP, SSH, ping, etc. all at the same time. 

## What happens when you type google.com into your web browser and hit enter?

1. DNS must resolve google.com to an IP address
    1. your computer checks its local DNS cache and hostfile to see if it needs to use its DNS server to resolve this (it is way faster if it doesn't)
    2. your computer forms a DNS request addressed to its configured DNS server (or secondary if the primary fails) with the appropriate headers. It sends the request over the network (a more detailed version of this will be later)
    3. The DNS server will check its own cache for the record. If it doesn't have it stored, it will
    4. query one of the root DNS servers. This will look at the top level domain (TLD) which is .com in this case. It will check with those nameservers for the authoritative name server for that TLD. This gets sent back to your local DNS server, which then
    5. queries the authoritative DNS servers for the TLD. That server will reply with the authoritative nameserver for that domain. (when you register a domain, you configure some authoritative nameservers with your registrar. These get stored on the TLD nameservers.) 
    6. Your local DNS server queries the authoritative nameserver.
    7. If an IP is returned (it is an A RECORD), it is done resolving the domain name, and returns it to your computer, then caches the record (your computer does this as well. they are cached based on the TTL configured) If a domain name is returned (it is a CNAME or alias) then the whole process goes again with the new domain name.

    If DNS fails, you will get an error in your browser that the DNS address could not be found

2. Now that your computer knows the destination IP for google.com, it starts forming the HTTP request. Since we are using a browser and navigating to a web page, the GET method is used (there are other methods used for different things). Some of these may not happen in the same order
    * The URI (NOT a URL) is put in the request.
    * A TCP 3-way handshake takes place
    * encryption keys are exchanged
    * The request is encrypted, then wrapped in a TCP segment (or multiple if it is too large)
    * the encrypted segment is encapsulated into a packet with the destination IP as the one from the DNS request. The port used is normally determined from the URI (443 for HTTPS, 80 for HTTP, though these protocols can go over any port if the server is listening for it). We will assume HTTPS. The source IP is decided by the OS. Since there can be multiple connections to the internet, the OS makes the decision on which interface is used to send the data. It also allocates a port for the browser to listen for a response. 
    *Assuming that you are not on the same network as google.com, you're gonna need a router for this one. An ARP request is made to ask the local subnet what the MAC is for the configured default gateway (router).
    * The router responds with its MAC address
    * The packet is encapsulated into an ethernet frame
    * The NIC reads the frame data from its buffer (it was put there by the CPU) and translates that to binary 1s and 0s which it transmits across the medium.
    * if there are switches involved on the way to the router, they do switch things TM and the frame makes it to the router.

3. The router removes the frame header, and checks CRC. If CRC fails, it drops the frame. TCP will handle lost frames at layer 4. Assuming this test passes, the router
    * checks its routing table to see if it has a route to the destination IP
    * if it doesn't, it will respond to your computer that there is no route to the host
    * if it does (including just a default route to another router), it puts a new frame header on the packet, does the ARP stuff, switch stuff happens if needed, physical stuff happens a lot, and the frame gets to another router. This happens until the router has an IP in the same subnet as the server IP in the destination IP. (it can tell based off of its own IP addresses and subnet masks)
    * the google router does the same thing and sends the packet to the server

4. The data is processed by the server
    1. The server checks the destination IP, and if it is assigned that IP, receives the packet into its NICs buffer
    2. data gets sent to the CPU. Low level CPU stuff like interrupts probably happen to make this work.
    3. everything gets deencapsulated and decrypted.
    4. if the OS is listening on the port, the data gets handed to the process listening on that port (should be some kind of webserver like Apache, NodeJS, Python Flask, etc.)
    5. The webserver checks for a file or endpoint associated with the GET request
    6. If there is an error with the request, an HTTP 4xx error is returned to the computer
    7. If there is a server error, an HTTP 5xx code is used
    8. HTTP redirects may happen (this starts a lot of the process over again to load the new site) e.g. www.google.com redirects to google.com.
    9. The webserver forms an HTML (or other filetype) response and associated headers.
    10. The data is encrypted, then encapsulated. Source port is swapped with destination port, and source IP is swapped with destination IP from the received packet.
    11. Routing and switching happens again to get the data back

    During the webserver's processing, it may make its own requests to other servers (such as an API). This can greatly speed up the page loading since a lot of discrete steps in processing can take place on seperate servers, taking the load off of the main webserver.

5. Your computer receives and processes the data
    1. If there is an error, it displays its built-in page for that error code. Issues with data not getting transmitted are handled by TCP, and are largely invisible to the user.
    2. The data gets handed to the browser process which then renders the HTML from the response.
    3. If there are external files referenced in the HTML, they are all loaded using this whole process over again for each one.
    4. JavaScript runs if needed (and may keep running)
    5. Cookies/localstorage are set if needed
    6. site files are cached for faster load times