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

<h3>Step 1: A‑Record Exercise</h3>

<p>From the Azure Portal -> Click on "Virtual Machines"</p>
<img width="1914" height="879" alt="image" src="https://github.com/user-attachments/assets/500beaf4-54da-42f5-b083-2f4bad6b63da" />
<br>
<p>Copy dc-1s Public IP Address</p>
<img width="1919" height="692" alt="image" src="https://github.com/user-attachments/assets/c02dfa84-f5af-410b-aea5-fdc3c031d0d7" />
<br>
<p>Go to Start ->Click "Windows + R" on the keyboard -> Type "mstsc" -> Click on "Ok"</p>
<img width="458" height="277" alt="image" src="https://github.com/user-attachments/assets/5238cb66-71ea-489e-ab3d-a7052323cebf" />
<br>
<p>Paste the Public Address -> Click on "Connect" -> Since it remembers my domain, just type in the Password -> Click on "Ok"</p>
<img width="1107" height="562" alt="image" src="https://github.com/user-attachments/assets/6f61c8a0-11ee-4f76-9749-f15f21cef112" />
<br>
<p>Click on "Yes"</p>
<img width="522" height="496" alt="image" src="https://github.com/user-attachments/assets/c90ae1b0-f39b-4dfc-b6e7-25a1f7237d7b" />
<br>
<p>From the Azure Portal -> Click on "Virtual Machines"</p>
<img width="1914" height="879" alt="image" src="https://github.com/user-attachments/assets/500beaf4-54da-42f5-b083-2f4bad6b63da" />
<br>
<p>Copy client-1s Public IP Address</p>
<img width="1913" height="690" alt="image" src="https://github.com/user-attachments/assets/03221662-f9d6-45f5-aada-248519b128e6" /> 
<br>
<p>Go to Start ->Click "Windows + R" on the keyboard -> Type "mstsc" -> Click on "Ok"</p>
<img width="458" height="277" alt="image" src="https://github.com/user-attachments/assets/5238cb66-71ea-489e-ab3d-a7052323cebf" />
<br>
<p>Logging into this client-1 as an Admin. Paste the Public Address -> Click on "Connect" -> Enter Admin Credentials -> Click on "Ok"</p>
<img width="1116" height="720" alt="image" src="https://github.com/user-attachments/assets/f3f528bd-e8df-4c26-a369-4b5ca75b5468" />
<br>
<p>Click on "Yes"</p>
<img width="522" height="496" alt="image" src="https://github.com/user-attachments/assets/c90ae1b0-f39b-4dfc-b6e7-25a1f7237d7b" />
<br>
<p>From "client-1" VM -> Go to start and type "cmd" -> Click on "Command Prompt"</p>
<img width="1000" height="943" alt="image" src="https://github.com/user-attachments/assets/80c759ae-5eaa-4f93-8410-02e145f64d70" />
<br>
<p>Type "ping mainframe". (Note that mainframe can be any name, it's just that it sounds cool, so I'm using it.) ->Click "Enter" on the keyboard. Notice the message shown in the yellow box. Attempted to ping mainframe from Client‑1 → failed (no DNS record).</p>
<img width="1488" height="774" alt="image" src="https://github.com/user-attachments/assets/22c7f845-f8dc-49e3-8204-cd893419789d" />
<br>
<p>Type "nslookup mianframe" -> Click "enter" on the keyboard. Verified with nslookup → no record found.</p>
<img width="1496" height="542" alt="image" src="https://github.com/user-attachments/assets/15f87ec0-3e3e-4ac5-ad9f-67fb5aac499f" />
<br>
<p>Created a DNS A‑record for mainframe pointing to DC‑1’s private IP. From "dc-1" -> Go to Start -> Expand "WIndows Admin Tools -> Click on "DNS" </p>
<img width="822" height="860" alt="image" src="https://github.com/user-attachments/assets/f5367033-ef10-4553-a808-35293c184c93" />
<br>
<p>Click on "dc-1" to expand -> Expand "Forward Lookup Zones" -> Click on "mydomain.com" to see its information.</p>
<img width="941" height="658" alt="image" src="https://github.com/user-attachments/assets/5a9d9d20-30a7-4830-9a4f-dd1efe19c163" />
<br>
<p>Right-Click "mydomain.com" -> Click on New Host</p>
<img width="945" height="668" alt="image" src="https://github.com/user-attachments/assets/35d1cd9e-a595-44ad-925d-df5fae3412df" />
<br>
<p>Type "mainframe" ->Type the dc-1s IP Adress -> Click on "Add Host"</p>
<img width="1067" height="659" alt="image" src="https://github.com/user-attachments/assets/7711d63b-6cd0-4688-9b4d-c36d8297481b" />
<br>
<p>Click "Ok"</p>
<img width="509" height="214" alt="image" src="https://github.com/user-attachments/assets/fe83bd07-fd72-4b04-ae3f-27609304287d" />
<p>Notice they both now have the same IP Address</p>
<img width="944" height="673" alt="image" src="https://github.com/user-attachments/assets/75f2e54d-7394-47ad-a4a7-26efc786e51c" />
<br>
<p>Go back to client-1 VM - > Go to the command prompt opened and try to ping "mainframe" again. Retested ping from Client‑1 and it was a success. </p>
<img width="1058" height="769" alt="image" src="https://github.com/user-attachments/assets/53875f02-31a8-4e76-a49b-e166b3b2e182" />
<br>

<h4>SUMMARY</h4>
Demonstrated how DNS A‑records map hostnames to IPs, enabling connectivity.

<h3>Step 2: Local DNS Cache Exercise</h3>

<p>Go to back to dc-1 and changed mainframe record on DC‑1 to point to 8.8.8.8. -> Click on "Ok"</p>
<img width="1442" height="689" alt="image" src="https://github.com/user-attachments/assets/fe331fbd-bf51-4659-9f28-e73ca72be92f" />
<img width="950" height="671" alt="image" src="https://github.com/user-attachments/assets/246e1909-af4b-4ecd-861a-3f9e09f35b3d" />
<br>
<p>Go back to client-1 -> try the ping command on cmd "ping mainframe" again to observe. Notice that client‑1 still pinged the old address due to cached entry.</p>
<img width="792" height="343" alt="image" src="https://github.com/user-attachments/assets/c9a96521-7875-4e17-847e-284d723a0a2a" />
<br> 
<p>Type in "ipconfig /displaydns" -> Click "enter" to observe -> type "ipconfig /displaydns > dns.txt" -> Click "Enter" (to create a text file on a notepad -> Type dns.txt (this will open and show the cache details on the notepad</p>
<img width="988" height="775" alt="image" src="https://github.com/user-attachments/assets/291d7fea-5ab6-4da0-b6b9-3efe50cd4ddf" />
<p>Local Cache still has the Old Address</p>
<img width="498" height="457" alt="image" src="https://github.com/user-attachments/assets/f542d11a-75ee-4616-a662-e30b15ec7f0e" />
<br>
<p>Flushed cache with ipconfig /flushdns. Go to Start -> Type "Powershell" -> Right-Click on Powershell -> Click on "Open as Administrator"</p>
<img width="979" height="952" alt="image" src="https://github.com/user-attachments/assets/aee3f553-7cdd-4655-a16d-17f7bc1cb155" />
<br>
<p>Type "ipconfig /flushdns" -> Click "Enter" on Keyboard</p>
<img width="1106" height="647" alt="image" src="https://github.com/user-attachments/assets/7580f432-4fc5-4f3f-9bad-8890191a251f" />
<br>
<p>No record of cache found for Mainframe. Type "ipconfig /displaydns -> Click "Enter" on Keyboard. To observe the dns cache again</p>
<img width="1110" height="639" alt="image" src="https://github.com/user-attachments/assets/c7a17361-72ea-4d7d-8500-0e6a0558e89b" />
<br> 
<p>Retested ping → new record resolved correctly. Go back to Command Propmt on client-1 and type "ping mainframe" to observe. </p>
<img width="807" height="342" alt="image" src="https://github.com/user-attachments/assets/93dbb2bf-187b-4ce2-83ca-7471dcd8345e" />
<br>
<h4>SUMMARY</h4>
Showed how local DNS caching can cause stale results and how flushing ensures accuracy.

3. CNAME Record Exercise
Created a CNAME record on DC‑1: search → www.google.com.

From Client‑1, pinged search → resolved to Google.

Verified with nslookup → confirmed CNAME resolution.
Operational Value: Demonstrates aliasing with CNAME records, useful for redirecting services or simplifying hostnames.



