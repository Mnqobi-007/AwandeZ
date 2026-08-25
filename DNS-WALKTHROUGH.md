DNS Walkthrough – Awande Zungu

FlyRank Internship Program – Phase Build (Core)

Live Portfolio: https://awandemz.netlify.app/

1. What is DNS?

DNS stands for Domain Name System. Its job is to translate human-friendly website names into information that computers can use to find the correct server.

For example, when I type:

awandemz.netlify.app


I don't need to know the server's IP address. DNS handles that lookup for me.

A simple way to think about DNS is like the contacts list on a phone. I can search for "Mom" instead of remembering Mom's phone number. DNS works in a similar way: I use a domain name, and DNS helps find the address associated with it.

So, at a high level:

Domain name → DNS lookup → IP address → Server


DNS is not responsible for sending the website itself. Its main job is to help the browser find where the website is hosted.

2. What is a CNAME Record?

A CNAME (Canonical Name) record is a type of DNS record that creates an alias from one hostname to another hostname.

For example, imagine I owned:

www.awandezungu.com


but wanted that hostname to point to:

awandemz.netlify.app


A CNAME could tell DNS:

www.awandezungu.com → awandemz.netlify.app


The important thing to understand is that a CNAME points to another hostname, not directly to an IP address.

DNS can then continue resolving the target hostname until it gets the address needed to connect to the host.

CNAME records are useful because I don't have to hard-code an IP address into my DNS configuration. If the hosting provider changes the IP addresses behind its hostname, the CNAME can continue pointing to the hostname while the provider manages those underlying changes.

For my current portfolio, I am using Netlify's provided hostname:

awandemz.netlify.app


If I later purchase a custom domain, I could configure DNS records so that my custom hostname points to my Netlify site.

3. What Actually Happens When I Visit a Website?

To understand DNS properly, it helps to follow the request from the moment I enter a website address until the website is displayed.

I'll use my portfolio as an example:

awandemz.netlify.app

Step 1: I enter the website address

I type:

https://awandemz.netlify.app


into my browser and press Enter.

The browser needs to find the server responsible for that hostname before it can request the website.

Step 2: The browser checks what it already knows

Before performing a complete DNS lookup, the browser or operating system may already have DNS information cached.

Caching exists to avoid doing the same lookup repeatedly.

If the required DNS information is already available and hasn't expired, the browser can use it rather than starting the lookup again.

If it doesn't have the information, the request is passed to a DNS resolver.

Step 3: The DNS resolver receives the request

The DNS resolver is the service that performs DNS lookups on behalf of the device.

This may be provided by an Internet Service Provider or a public DNS service such as Google Public DNS or Cloudflare.

I can think of the resolver as the person I ask:

"I need to find the address for awandemz.netlify.app. Can you look it up for me?"

The resolver checks its own cache first. If it doesn't already know the answer, it starts querying the DNS hierarchy.

4. The DNS Hierarchy

The resolver may need to work through several levels of DNS servers.

For my domain:

awandemz.netlify.app


the important parts are:

awandemz   .   netlify   .   app
   ↑             ↑          ↑
hostname      domain      TLD


The resolver can work through the hierarchy to find the authoritative answer.

Step 4: The resolver asks a root nameserver

The first level is the DNS root.

The root servers don't normally have the final answer for my specific hostname.

Instead, they know where to find information about top-level domains.

Because my hostname ends in:

.app


the root directs the resolver toward the nameservers responsible for the .app top-level domain.

There are 13 root server identities, operated from many locations around the world. The "13" refers to the named root server identities, not literally only 13 physical machines.

Step 5: The resolver asks the .app TLD nameserver

The resolver then asks a Top-Level Domain (TLD) nameserver about:

netlify.app


The .app nameservers are responsible for information about domains underneath .app.

They don't necessarily contain the final IP address for my portfolio.

Instead, they can tell the resolver which authoritative nameservers are responsible for the netlify.app domain.

Step 6: The resolver asks the authoritative nameserver

This is where the resolver gets closer to the actual answer.

An authoritative nameserver is a DNS server that has the authoritative DNS records for a particular domain.

The resolver asks it for the DNS record associated with:

awandemz.netlify.app


The authoritative DNS system returns the record it has for that hostname.

Depending on the configuration, this could ultimately lead to an IP address or another hostname that needs to be resolved further.

The important distinction is:

Resolver: finds the answer on behalf of the client.
Nameserver: provides DNS information.
Authoritative nameserver: provides the official DNS information for a domain.
5. The DNS Record Is the Actual Answer

DNS is made up of different types of records.

Some common examples are:

Record	Purpose
A	Maps a hostname to an IPv4 address
AAAA	Maps a hostname to an IPv6 address
CNAME	Makes one hostname an alias of another hostname
MX	Specifies mail servers for a domain
TXT	Stores text information, often used for verification and security

For example, an A record could conceptually look like:

example.com → 203.0.113.10


A CNAME could look like:

www.example.com → example.host.com


The exact records used by a real hosting provider depend on how that provider has configured its infrastructure.

6. The Resolver Returns the Answer

Once the resolver has found the required DNS information, it returns the result to my computer.

The resolver may also cache the result according to the record's TTL (Time To Live).

Caching is important because thousands or millions of users may request the same domain. There is no reason for every request to repeat the entire DNS lookup from the beginning.

So the simplified process is:

Browser
   ↓
DNS Resolver
   ↓
Root
   ↓
.app TLD
   ↓
Authoritative Nameserver
   ↓
DNS Record
   ↓
Resolver
   ↓
Browser

7. DNS Is Finished — Now the Browser Connects

This is an important part of understanding DNS.

DNS does not deliver the website.

DNS helps the browser discover where to connect.

Once the browser has the necessary address information, it can establish a connection to the hosting infrastructure.

Because my portfolio uses HTTPS, the browser establishes a secure HTTPS connection and sends an HTTP request for the website.

Conceptually:

DNS:
"What address should I connect to?"

HTTPS/HTTP:
"Now that I know where to connect, give me the website."


The host then processes the request and sends the appropriate response.

8. The Host Responds

The browser sends an HTTPS request asking for the website.

The hosting infrastructure responds with the resources required to display the page, such as:

HTML
CSS
JavaScript
Images
Other assets


The browser receives those files and begins rendering the page.

That is why DNS is only one part of the complete journey.

The overall process is:

Enter domain
     ↓
DNS lookup
     ↓
Find destination
     ↓
Establish HTTPS connection
     ↓
Send HTTP request
     ↓
Host processes request
     ↓
Host returns response
     ↓
Browser renders website

9. The Complete Journey

Putting everything together, when someone visits:

https://awandemz.netlify.app


the simplified journey looks like this:

1. User enters awandemz.netlify.app
                    ↓
2. Browser/OS checks DNS cache
                    ↓
3. DNS resolver receives the lookup request
                    ↓
4. Resolver checks its own cache
                    ↓
5. Resolver queries the DNS hierarchy if necessary
                    ↓
6. Root points toward the .app TLD
                    ↓
7. .app TLD identifies the authoritative DNS
                    ↓
8. Authoritative nameserver provides the DNS record
                    ↓
9. Resolver returns the result to the client
                    ↓
10. Browser knows where to connect
                    ↓
11. Browser establishes HTTPS connection
                    ↓
12. Browser sends an HTTP request
                    ↓
13. Host returns the website resources
                    ↓
14. Browser renders the portfolio

10. Why Understanding DNS Matters to Me

Understanding DNS is useful because it allows me to troubleshoot problems instead of simply assuming that "the website is down."

For example, if a website isn't loading, I can start thinking about different layers of the process:

Is DNS resolving correctly?
        ↓
Is the hostname pointing to the expected destination?
        ↓
Can the browser establish a connection?
        ↓
Is HTTPS working correctly?
        ↓
Is the host responding to the HTTP request?
        ↓
Is the application itself working?


This gives me a structured way to investigate problems.

It also helps me understand how custom domains work.

If I eventually purchase something like:

awandezungu.com


I will need to configure DNS so that the appropriate hostname points to my hosting provider.

I now understand that this isn't simply "changing the website address." There is a DNS layer that connects the human-friendly domain name to the infrastructure serving the website.

11. What I Understand From This

The main thing I take away from DNS is that the domain name and the website server are two different things.

The domain name is the human-friendly name.

DNS provides the lookup system that connects that name to the information needed to find the destination.

The resolver performs the lookup, the DNS hierarchy helps it find the correct authoritative source, the authoritative nameserver provides the relevant DNS record, and the browser then uses the result to connect to the host.

So, in simple terms:

DNS helps the browser find where a website is. HTTPS and HTTP are then used to communicate with that host and retrieve the website.

That distinction is important because it means I can reason about DNS problems separately from hosting or application problems.

12. Final Summary

When someone types my portfolio address:

awandemz.netlify.app


the browser doesn't automatically know where the website is hosted.

It first needs to resolve the hostname.

A DNS resolver performs that lookup, potentially working through the root, the .app TLD nameservers, and the authoritative DNS infrastructure until it gets the relevant record.

The resolver returns the result, and the browser can then establish an HTTPS connection to the destination.

The host receives the request and returns the website resources, which the browser renders into the page the user sees.

In one line:

Domain name → Resolver → DNS hierarchy → Authoritative record → Destination → HTTPS → Host response → Website


This is my understanding of how DNS connects a human-readable website address to the infrastructure that serves the website.

Author: Awande Zungu
Program: FlyRank Internship Program – Phase Build (Core)
Portfolio: https://awandemz.netlify.app/
