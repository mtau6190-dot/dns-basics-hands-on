<p align="center">
<img src="https://copilot.microsoft.com/th/id/BCO.07b72dfe-fbb8-4bf7-8e30-b0dccdba9f1c.png" alt="DNS Resolution Diagram"/>
</p>

<h1>Building an Intuition for DNS</h1>
Project Summary:<br />
<br />
To gain practical understanding of how DNS records work (A‑records, CNAMEs, and local DNS cache) by configuring and testing them in a domain environment.<br />

<h2>Environment</h2>

<h3>This DNS lab was conducted entirely within Microsoft Azure, using virtual machines configured in a private domain network:</h3>

- DC‑1 (Domain Controller): Hosted on Azure VM, running Active Directory DNS
- Client‑1 (Domain-joined workstation): Hosted on Azure VM
- Azure Resource Group: Used to organize and manage all related resources
- Virtual Network (VNet): Custom subnet for domain traffic and DNS resolution
- Azure Portal: Used for provisioning, monitoring, and managing VM connectivity
<p>This setup allowed for isolated testing of DNS records, cache behavior, and name resolution, all within a scalable cloud environment.</p>

<h2>Exercises</h2>

<h3> 1. A‑Record Exercise</h3>
  
- Attempted to ping mainframe from Client‑1 → failed (no DNS record).
- Verified with nslookup → no record found.
- Created a DNS A‑record for mainframe pointing to DC‑1’s private IP.
- Retested ping from Client‑1 → success.
- Operational Value: Demonstrates how DNS A‑records map hostnames to IPs, enabling connectivity.

2. Local DNS Cache Exercise
Changed mainframe record on DC‑1 to point to 8.8.8.8.

Client‑1 still pinged the old address due to cached entry.

Observed cache with ipconfig /displaydns.

Flushed cache with ipconfig /flushdns.

Retested ping → new record resolved correctly.
Operational Value: Shows how local DNS caching can cause stale results and how flushing ensures accuracy.

3. CNAME Record Exercise
Created a CNAME record on DC‑1: search → www.google.com.

From Client‑1, pinged search → resolved to Google.

Verified with nslookup → confirmed CNAME resolution.
Operational Value: Demonstrates aliasing with CNAME records, useful for redirecting services or simplifying hostnames.



