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

================================================================================

3. WHAT HAPPENS WHEN YOU VISIT A WEBSITE?

Let me walk you through what happens when someone types "awandemz.netlify.app"
into their browser:

STEP 1: You Type the Address
You open your browser and type "awandemz.netlify.app" into the address bar and
press Enter.

STEP 2: The Browser Checks Its Cache
Your browser first checks its own memory (cache) to see if it already knows the
IP address for this site. If it visited recently, it might remember and skip the
rest of the steps.

STEP 3: The Resolver Asks Around
If the browser doesn't know the address, it asks your DNS resolver. This is
usually provided by your internet provider (like Vodacom, Telkom, or Rain) or a
service like Google DNS (8.8.8.8). The resolver is like a librarian who knows
where to find information.

STEP 4: The Resolver Queries the Nameservers
The resolver asks a series of servers in a specific order:

a) Root Nameserver
   The top-level server. There are only 13 root servers in the world. It doesn't
   know the exact address, but it knows who to ask next. It looks at the ".app"
   part and points the resolver to the .app TLD nameserver.

b) TLD Nameserver (Top-Level Domain)
   This server handles the ".app" part of the address. It knows which nameserver
   is responsible for "netlify.app" subdomains and points the resolver to
   Netlify's authoritative nameserver.

c) Authoritative Nameserver
   This is the final stop. Netlify's authoritative nameserver has the exact
   record for "awandemz.netlify.app". It looks up the record and finds the IP
   address for the server hosting the site, such as "75.2.60.5".

STEP 5: The Resolver Gets the Answer
The authoritative nameserver sends back the IP address to the resolver.

STEP 6: The Resolver Tells Your Browser
Your resolver sends the IP address back to your browser. Your browser now knows
exactly where to go.

STEP 7: Your Browser Connects to the Server
Now that your browser knows the IP address, it establishes a secure connection
to that server using HTTPS.

STEP 8: The Server Responds
The browser sends an HTTPS request asking for the website files. The server
responds by sending back the HTML, CSS, and JavaScript files.

STEP 9: The Browser Renders the Page
Your browser reads the files, assembles them, and displays the page you see.

STEP 10: The Browser Caches the Result
Your browser stores the IP address so future visits are much faster.

================================================================================

4. SUMMARY – THE JOURNEY IN SIMPLE TERMS

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

5. WHY THIS MATTERS FOR THIS ASSIGNMENT

Understanding DNS helps me:

- Troubleshoot issues (if my site goes down, I can check if it's a DNS problem
  or a server problem)
- Use custom domains in the future (if I buy "awandezungu.com", I'll know how to
  point it to Netlify)
- Understand how the internet works at a fundamental level
- Show that I know web infrastructure, not just coding

For this project, I'm using Netlify's free domain (awandemz.netlify.app). If I
later want a custom domain, I'll add a CNAME record pointing to Netlify.

================================================================================

Written by Awande Zungu for the FlyRank Internship Program – Phase Build (core)
Live Portfolio: https://awandemz.netlify.app/
