<p align="center">
<img src="https://github.com/user-attachments/assets/7c526d0a-1014-467d-b658-4b485f6a94fd" alt="DNS"/>
</p>

<h1 align="left">Basic DNS Demonstration and Testing Lab</h1>

<p>This lab demonstrates DNS functionality by testing A-record creation, local DNS cache behavior, and CNAME records within a domain environment. We will perform specific tests on DNS resolution, cache management, and aliasing using CNAME records.</p>

<h2>Tosin Eluyera - Portfolio Project</h2>

<h2>Technologies and Environments Used</h2>
<ul>
  <li><strong>Microsoft Azure:</strong> Used to host the virtual machines (DC-1 and Client-1).</li>
  <li><strong>Windows Server 2022:</strong> Operating system on the Domain Controller (DC-1).</li>
  <li><strong>Windows 10:</strong> Operating system on the client machine (Client-1).</li>
  <li><strong>Remote Desktop:</strong> Used to access and manage the virtual machines.</li>
  <li><strong>DNS (Domain Name System):</strong> Network service to resolve domain names to IP addresses.</li>
  <li><strong>A-Records:</strong> Used to associate a hostname with an IP address within the DNS system.</li>
  <li><strong>CNAME (Canonical Name) Records:</strong> DNS records used to create an alias for another domain name, allowing one domain to point to another.</li>
  <li><strong>DNS Cache:</strong> Stores DNS query results locally to speed up subsequent access to the same domain name.</li>
</ul>

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>A-Record Exercise</h2>
<ol>
  <li>Log into DC-1 as your domain admin account (<code>mydomain.com\jane_admin</code>).</li>
  <li>Log into Client-1 as an admin (<code>mydomain\jane_admin</code>).</li>
  <li>From Client-1, attempt to ping “mainframe”. Observe that the ping fails since no DNS record exists for "mainframe".</li>
   <img src="https://i.imgur.com/Qd7o2WX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Run an <code>nslookup</code> on “mainframe” from Client-1. Notice that it fails because no DNS A-record has been created for the hostname.</li>
  <li>On DC-1, create a DNS A-record for “mainframe” and point it to DC-1’s Private IP address. This creates an entry in DNS that associates "mainframe" with DC-1's IP.</li>
   <img src="https://i.imgur.com/0s9jRZj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <img src="https://i.imgur.com/9y8tJUL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Return to Client-1 and ping “mainframe” again. The ping should now succeed, as the DNS A-record has been created and is resolving to the correct IP.</li>
  <img src="https://i.imgur.com/4jfY0Qq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</ol>

<h2>Local DNS Cache Exercise</h2>
<ol>
  <li>On DC-1, modify the “mainframe” A-record, changing its IP address to <code>8.8.8.8</code>, Google's public DNS server address.</li>
  <img src="https://i.imgur.com/guPqRVq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Go back to Client-1 and attempt to ping “mainframe” again. Notice that it still resolves to the old IP address, as the DNS entry is cached locally on Client-1.</li>
  <img src="https://i.imgur.com/4jfY0Qq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>On Client-1, display the local DNS cache by running <code>ipconfig /displaydns</code>. This shows the cached DNS entries stored on the client.</li>
  <img src="https://i.imgur.com/incJFLd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Flush the DNS cache on Client-1 using <code>ipconfig /flushdns</code>. This clears the locally cached entries.</li>
  <img src="https://i.imgur.com/ZihNAdB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Ping “mainframe” again and observe that the ping now resolves to the updated IP address, as the client is no longer relying on cached data.</li>
  <img src="https://i.imgur.com/CMbYAn6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</ol>

<h2>CNAME Record Exercise</h2>
<ol>
  <li>On DC-1, create a CNAME record that points the alias “search” to <code>www.google.com</code>. CNAME records create aliases for hostnames, allowing one domain to refer to another.</li>
   <img src="https://i.imgur.com/DYNOSKz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>Return to Client-1 and ping “search”. The ping should resolve to the IP address of <code>www.google.com</code>, demonstrating the functionality of the CNAME record.</li>
   <img src="https://i.imgur.com/h719A4d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  <li>On Client-1, run <code>nslookup</code> for “search” and observe that it resolves to <code>www.google.com</code>, confirming the CNAME record is working correctly.</li>
  <img src="https://i.imgur.com/Yoo790j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</ol>

<h2>Conclusion</h2>
<p>In this lab, we explored several critical DNS functions. We started by creating an A-record on our Domain Controller, allowing the "mainframe" hostname to resolve to an IP address. We then experimented with local DNS caching on the client machine, observing how cached DNS entries can persist until flushed. Finally, we set up a CNAME record, demonstrating how aliasing works in DNS by redirecting a hostname to another domain.</p>

<p>These exercises demonstrated the importance of DNS in network environments, especially for name resolution and how DNS caching and record types like A-records and CNAMEs operate in a domain environment.</p>
