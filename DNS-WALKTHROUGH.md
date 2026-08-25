# DNS Walkthrough: How Websites Work

## What is DNS?

DNS stands for **Domain Name System**. Think of it as the internet's phonebook. 

When you want to call someone, you use their name (like "Mom") instead of memorizing their phone number. Your phone then looks up that name and dials the right number. DNS does the same thing for websites.

Instead of remembering complicated numbers like `192.168.1.1`, you just type something easy like `google.com` or `awandemz.netlify.app`. DNS translates that human-friendly name into the computer-friendly IP address that tells your browser where to find the website.

## What is a CNAME Record?

A **CNAME** (Canonical Name) record is like a nickname or alias for a website.

For example, if I own `awandezungu.com` but my website is hosted on GitHub Pages at `awandemz.netlify.app`, I can create a CNAME record that tells the internet: "Whenever someone types `awandezungu.com`, send them to `mnqobi-007.github.io` instead."

CNAME records are useful because:
- They let you use a custom domain name without moving your hosting
- You can change hosting providers without updating your main domain
- They're easier to manage than IP addresses (which can change)

## What Happens When You Visit a Website?

Let me walk you through what happens when someone types `mnqobi-007.github.io` into their browser:

### Step 1: You Type the Address
You open your browser and type `mnqobi-007.github.io` into the address bar and press Enter.

### Step 2: The Browser Checks Its Cache
Your browser first checks its own memory (cache) to see if it already knows the IP address for this site. If it visited the site recently, it might remember and skip the rest of the steps.

### Step 3: The Resolver Asks Around
If the browser doesn't know the address, it asks your **DNS resolver**. This is usually provided by your internet provider (like Vodacom, Telkom, etc.) or a service like Google DNS (`8.8.8.8`). The resolver is like a librarian who knows where to find information.

### Step 4: The Resolver Queries the Nameservers
The resolver starts asking a series of servers:

1. **Root Nameserver** — This is the top-level server. It doesn't know the exact address, but it knows who to ask next. It points the resolver to the `.github.io` nameserver.

2. **TLD Nameserver** (Top-Level Domain) — This server handles the `.io` part of the address. It knows which nameserver is responsible for `github.io` subdomains.

3. **Authoritative Nameserver** — This is the final stop. GitHub's authoritative nameserver has the exact record for `mnqobi-007.github.io`. It looks up the DNS record and finds the IP address for the server hosting the site.

### Step 5: The Resolver Gets the Answer
The authoritative nameserver sends back the IP address to the resolver. For GitHub Pages, this might be something like `185.199.108.153`.

### Step 6: The Resolver Tells Your Browser
Your resolver sends the IP address back to your browser.

### Step 7: Your Browser Connects to the Server
Now that your browser knows the IP address, it connects to that server and asks for the website files.

### Step 8: The Server Responds
The server sends back the HTML, CSS, and JavaScript files that make up the website. Your browser reads these files and displays the page you see.

### Step 9: The Browser Caches the Result
Your browser stores the IP address in its cache so that future visits will be much faster.

## Putting It All Together

Here's a simple way to remember the flow:
