# Recursive DNS

> A recursive DNS lookup is where one DNS server communicates with several other DNS servers to hunt down an IP address and return it to the client

* This is in contrast to an iterative DNS query, where the client communicates directly with each DNS server involved in the lookup
* Recursive DNS queries generally tend to resolve faster than iterative queries. This is due to caching.
* This method can enable attackers to perform **DNS amplification attacks** and **DNS cache poisoning**

## DNS Amplification Attacks
* An attacker uses a group of machines (known as a **botnet**) to send a high volume of DNS queries using a **spoofed** IP address.
    - The attacker is sending requests from their own IP, but asking the responses to go the victim
    - In order to exacerbate the attack, the spoofed request asks for a very long response.
    - The victimized service will receive a flood of lengthy and unwanted DNS responses that can disrupt or even take down their servers.
* A recursive DNS server is needed to carry out this kind of attack, because the amplified DNS packets are responses to recursive DNS queries

## DNS Cache Poisoning Attacks
* When a recursive DNS server requests an IP address from another DNS server, an attack intercepts the request and gives a fake response.
* Not only does the recursive DNS server send the original client this IP address, but the server will also save the response in its cache.
* Any user that requests an IP for the same domain name will be sent to the malicious website
* In an iterative DNS query, the client directly asks each DNS server for the answer. Even if an attacker is able to send a forged response to the query,
it will only affect a **single** client.
