DNS Walkthrough – Awande Zungu
FlyRank Internship Program – Phase Build (core)
Live Portfolio: https://awandemz.netlify.app/
================================================================================

1. WHAT IS DNS?

DNS stands for Domain Name System. Think of it as the internet's phonebook.

When you want to call someone, you use their name (like "Mom") instead of
memorizing their phone number. Your phone looks up that name and dials the right
number. DNS does the same thing for websites.

Instead of remembering complicated numbers like "75.2.60.5", you just type
something easy like "awandemz.netlify.app". DNS translates that human-friendly
name into the computer-friendly IP address that tells your browser where to find
the website.

Without DNS, we would all have to memorize long strings of numbers just to visit
our favourite websites. DNS makes the internet usable for everyone.

================================================================================

2. WHAT IS A CNAME RECORD?

A CNAME (Canonical Name) record is like a nickname or alias for a website.

For example, if I own "awandezungu.com" but my website is hosted on Netlify at
"awandemz.netlify.app", I can create a CNAME record that tells the internet:
"Whenever someone types 'awandezungu.com', send them to 'awandemz.netlify.app'
instead."

CNAME records are useful because:
- They let you use a custom domain name without moving your hosting
- You can change hosting providers without updating your main domain
- They're easier to manage than IP addresses (which can change)
- They allow multiple domain names to point to the same website

A CNAME record is different from an A record. An A record points directly to an
IP address, while a CNAME record points to another domain name.

================================================================================

3. WHAT HAPPENS WHEN YOU VISIT A WEBSITE?

Let me walk you through exactly what happens when someone types
"awandemz.netlify.app" into their browser:

STEP 1: You Type the Address
You open your browser and type "awandemz.netlify.app" into the address bar and
press Enter.

STEP 2: The Browser Checks Its Cache
Your browser first checks its own memory (cache) to see if it already knows the
IP address for this site. If it visited recently, it might remember and skip the
rest of the steps. This caching makes the web feel fast and responsive.

STEP 3: The Resolver Asks Around
If the browser doesn't know the address, it asks your DNS resolver. This is
usually provided by your internet provider (like Vodacom, Telkom, or Rain) or a
service like Google DNS (8.8.8.8) or Cloudflare DNS (1.1.1.1).

The resolver is like a librarian who knows where to find information. It doesn't
know the answer itself, but it knows exactly who to ask.

STEP 4: The Resolver Queries the Nameservers
The resolver asks a series of servers in a specific order:

a) Root Nameserver
   This is the top-level server. There are only 13 root servers in the world,
   managed by different organizations. It doesn't know the exact address, but it
   knows who to ask next. It looks at the ".app" part of the address and points
   the resolver to the .app TLD nameserver.

b) TLD Nameserver (Top-Level Domain)
   This server handles the ".app" part of the address. TLDs include .com, .org,
   .io, .app, .net, and many others. It knows which nameserver is responsible
   for "netlify.app" subdomains and points the resolver to Netlify's
   authoritative nameserver.

c) Authoritative Nameserver
   This is the final stop. Netlify's authoritative nameserver has the exact
   record for "awandemz.netlify.app". It looks up the specific DNS record and
   finds the IP address for the server hosting the site, such as "75.2.60.5".

STEP 5: The Resolver Gets the Answer
The authoritative nameserver sends back the IP address to the resolver. This is
called a DNS response.

STEP 6: The Resolver Tells Your Browser
Your resolver sends the IP address back to your browser. Your browser now knows
exactly where to go.

STEP 7: Your Browser Connects to the Server
Now that your browser knows the IP address, it establishes a secure connection
to that server using HTTPS. This ensures all data exchanged is encrypted and
secure.

STEP 8: The Server Responds
The browser sends an HTTPS request asking for the website files. The server
responds by sending back the HTML, CSS, and JavaScript files that make up the
website. Images and other assets are also downloaded.

STEP 9: The Browser Renders the Page
Your browser reads the HTML, CSS, and JavaScript files, assembles them, and
displays the page you see. This is called rendering.

STEP 10: The Browser Caches the Result
Your browser stores the IP address and some website files so that future visits
are much faster. This caching happens at multiple levels: browser cache,
operating system cache, ISP cache, and local network cache.

================================================================================

4. SUMMARY – THE JOURNEY IN SIMPLE TERMS

Here's a simple way to understand the entire process:

   You type awandemz.netlify.app
                ↓
   Browser checks its memory (cache)
                ↓
   Browser asks the DNS resolver
                ↓
   Resolver asks: Root → .app TLD → Netlify's nameserver
                ↓
   Netlify's nameserver returns the IP address (e.g., 75.2.60.5)
                ↓
   Resolver gives the IP to your browser
                ↓
   Browser connects to the server at that IP over HTTPS
                ↓
   Server sends the website files (HTML, CSS, JS)
                ↓
   Website appears in your browser

================================================================================

5. REAL-WORLD EXAMPLE

Let's trace this with my actual portfolio site:

1. You type: awandemz.netlify.app
2. Browser cache: Checks if it knows the IP. (First time? Probably not.)
3. Resolver: Your ISP's DNS server receives the query
4. Root server: "I don't know, but ask the .app TLD server"
5. .app TLD server: "I don't know, but Netlify's nameservers handle .netlify.app"
6. Netlify's nameserver: "awandemz.netlify.app points to 75.2.60.5"
7. Resolver: Sends 75.2.60.5 back to your browser
8. Browser: Connects to 75.2.60.5 via HTTPS
9. Netlify's server: Sends my HTML, CSS, and JavaScript files
10. You see: My portfolio website

================================================================================

6. WHY THIS MATTERS FOR THIS ASSIGNMENT

Understanding DNS helps me:

- Troubleshoot issues: If my site goes down, I can check if it's a DNS problem
  or a server problem
- Use custom domains: If I buy "awandezungu.com" in the future, I'll know
  exactly how to point it to Netlify using a CNAME record
- Understand the internet: DNS is a fundamental technology that makes the web
  work. Understanding it shows I know web infrastructure, not just coding
- Stand out in interviews: Knowing this stuff demonstrates real-world technical
  knowledge

For this project, I'm using Netlify's free domain: awandemz.netlify.app

If I later want a custom domain like awandezungu.com, I would:
1. Buy the domain from a registrar
2. Go to Netlify site settings → Domain management
3. Add the custom domain in Netlify
4. Update DNS records at my registrar to add a CNAME record pointing to
   awandemz.netlify.app
5. Wait for propagation (up to 48 hours)
6. Verify HTTPS is working correctly

Now that I understand DNS, I could do all of this confidently instead of just
blindly following a tutorial.

================================================================================

Written by Awande Zungu for the FlyRank Internship Program – Phase Build (core)
Live Portfolio: https://awandemz.netlify.app/
Date: 25 August 2026
