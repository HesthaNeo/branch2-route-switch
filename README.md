<p align="center">
<img width="592" height="182" alt="Screenshot 2026-04-17 003809" src="https://github.com/user-attachments/assets/169d7d38-a238-4479-9b1e-9f8aa5dc9b0a" />
</p>
<h1><u>Milestone 11: Branch 2 Route/Switch</u></h1>
    <p>Tenth phase, we will install  1 CISCO1941/K9 router with ipbasek9, and securityk9 licensing. This router will act as the Branch 2 gateway providing access back to HQ and Branch 1 via a Site to Site (L2L) VPN  over the Internet. In addition, we'll install a Cisco WS-C2960-24TT layer 2 access switch.</p>
    <h2><strong><u>Configuration Steps</u></strong></h2>
    <p><b>Step 1: Install And Configure The Branch 2 Router</b></p>
        <p>- A. Rack, Mount, And Power On The Cisco 1941 Router</p>
        <p>- B. Install Securityk9 License</p>
        <p>- C. Basic Router Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</p>
        <p>- D. Configure And Connect Branch 2 LAN Interface G0/0</p>
            <p>- I. MGMT Interface VLAN 100</p>
            <p>- II. Data Interface VLAN 192</p>
            <p>- III. Voice Interface VLAN 10</p>
        <p>- E. Configure DHCP Services For Branch 2 Data And Voice Networks</p>
            <p>- I. Address Exclusions</p>
            <p>- II. DHCP Pool B2-DATA</p>
                <p>- 1. Network</p>
                <p>- 2. Default-Router</p>
                <p>- 3. DNS Server</p>
            <p>- III. DHCP Pool B2-VOICE</p>
                <p>- 1. Network</p>
                <p>- 2. Default-Router</p>
                <p>- 3. Option 150 IP</p>
        <p>- F. Configure IPSec/Isakmp VPN Policy And Cryptography</p>
            <p>- I. HQ Traffic Access List</p>
            <p>- II. Isakmp Policy</p>
            <p>- III. Isakmp Key</p>
            <p>- IV. Ipsec SA Lifetime And Transform-Set</p>
            <p>- V. Ipsec-Isakmp Crypto Map</p>
        <p>- G. Configure Access-list To Allow Only VPN Traffic From Branch 2</p>
        <p>- H. Configure and connect Internet interface G0/1</p>
            <p>- I. IP Address</p>
            <p>- II. Disable CDP</p>
            <p>- III. Apply VPN Only Access-List Inbound</p>
            <p>- IV. Apply VPN Crypto Map For Branch 2 VPN</p>
        <p>- I. Configure Static Routes</p>
            <p>- I. Route Pointing The HQ Public IP Address To The Internet Gateway Public IP</p>
            <p>- II. Default Route Pointing To The HQ Public IP Address</p>
    <p><b>Step 2: Install and Configure The Branch 2 Switch</b></p>
        <p>- A. Rack, Mount, And Power On All Three Switches</p>
        <p>- B. Basic Router Configurations (Hostname, NTP, Domain-Name, SSH, Etc)</p>
        <p>- C. Configure VLAN Trunking Protocol (VTP) Transparent</p>
        <p>- D. Configure MGMT VLAN Interface</p>
        <p>- E. Configure Default Gateway</p>
        <p>- F. Configure And Connect Trunks Port Back To The Branch 1 Router</p>
        <p>- G. Configure Access Ports</p>
        <h2><strong><u>Implementation</u></strong></h2>
        <h3>Step 1: Install And Configure The Branch 1 Router</h3>
            <p>- A. First, we will rack, mount, and power on the cisco 1941 router.</p>
                <img width="1175" height="933" alt="Screenshot 2026-04-18 172128" src="https://github.com/user-attachments/assets/c02a4580-6c94-479d-9b50-585cd0ec4643" />
            <p>- B. Next, we will install the securityk9 license.</p>
                <img width="870" height="944" alt="Screenshot 2026-04-18 172455" src="https://github.com/user-attachments/assets/8569a47a-8040-4679-a3f4-56330a8a1c81" />
                <img width="873" height="1395" alt="Screenshot 2026-04-18 172622" src="https://github.com/user-attachments/assets/1ed8e1d2-3068-47ab-a2af-948c9ba3d21b" />
                <img width="871" height="1175" alt="Screenshot 2026-04-18 172712" src="https://github.com/user-attachments/assets/f8ddf371-ce69-44fa-a872-52d1bf3db8ac" />
            <p>- C. Next we will do basic Router configurations (hostname, NTP, domain-name, SSH, etc).</p>
                <img width="871" height="983" alt="Screenshot 2026-04-18 172906" src="https://github.com/user-attachments/assets/63635da3-a14e-4d91-bffb-871d57521e3a" />
            <p>- D. Now, we'll configure and connect branch 2 LAN interface G0/0. We'll set our VLANS respectively as well. (Mgmt interface vlan 100, data interface vlan 192, voice interface vlan 10.)</p>
                <img width="870" height="869" alt="Screenshot 2026-04-18 173258" src="https://github.com/user-attachments/assets/66590791-6acd-4933-a61d-dc846e396de7" />
            <p>- E. Next, we'll configure DHCP services for branch 2 data and voice networks.</p>
                1. First, address exclusions for the DCHP pools.
                <img width="873" height="266" alt="Screenshot 2026-04-18 173707" src="https://github.com/user-attachments/assets/d479b484-8db3-445a-9a57-eff7ca95c783" />
                2. Second, we'll configure the DHCP pool for B2-data (network, default-router, dns server, etc.)
                <img width="875" height="286" alt="Screenshot 2026-04-18 174003" src="https://github.com/user-attachments/assets/8ec1b9fd-86d6-4631-8661-24d606f7cd8a" />
                3. Lastly, we'll configure the DHCP pool for B2-voice.
                <img width="869" height="380" alt="Screenshot 2026-04-18 174325" src="https://github.com/user-attachments/assets/8b5cce79-496d-4a18-a7aa-240b1a2d6f10" />
                <p><em>- The option "150 command" adds the TFTP option to make the phones register with HQ-VOICE-RT. Also no DNS server is required to be handed out to the phones on the network.</em></p>
            <p>- F. For this next step, we'll set up the VPN policy and cyrpto map for the IPSec site-to-site VPN to HQ.</p>
                1. We'll start by creating an ACL for the crypto map that matches any traffic going to HQ networks:
                <img width="873" height="288" alt="Screenshot 2026-04-18 174941" src="https://github.com/user-attachments/assets/fe71856f-c1cd-41e5-8043-ada16eb93e84" />
                2. Second, we'll configure the ISAKMP policy.
                <img width="871" height="304" alt="Screenshot 2026-04-18 175301" src="https://github.com/user-attachments/assets/ef6b976d-e0d2-4870-bad1-594430261b33" />
                3. Third, we'll configure the IPSec SA lifetime and Transform Set.
                <img width="870" height="236" alt="Screenshot 2026-04-18 180139" src="https://github.com/user-attachments/assets/3e798979-1f44-4ae6-a784-e2bda6512ee3" />
            <p>- G. Next, we'll configure private WAN border gateway protocol (BGP) peering.</p>
                1. We'll start by configuring the BGP router ID and set up peering with the provider router.
                <img width="869" height="243" alt="Screenshot 2026-04-16 165712" src="https://github.com/user-attachments/assets/9d88ca45-7162-4080-8041-9427d952251f" />
                <p><em>- Command "router bgp 65123" starts so we can enter the configuration for autonomous system #65123. Command "bgp router-id 192.168.250.6" forces the router to us g0/1 IP as the BGP ID. Command "neighbor 192.168.250.5 remote-as 65535" configures the BGP peer.</em></p>
                2. Second, we'll configure network statements to advertise across the private WAN.
                <img width="870" height="1094" alt="Screenshot 2026-04-16 170216" src="https://github.com/user-attachments/assets/4cbe6e60-4d19-45a2-b592-172574edbecb" />
                <p><em>- "network 192.168.120.0 mask 255.255.255.0" advertises B1 MGMT, "network 192.168.20.0 mask 255.255.255.0" advertises B1 DATA, "network 10.10.20.0 mask 255.255.255.0" advertises B1 VOICE.</em></p>
                <p><em>- Let's check the bgp neighbor to make sure it is connected:</em></p>
                <img width="874" height="365" alt="Screenshot 2026-04-16 170610" src="https://github.com/user-attachments/assets/cbf3841e-e22b-4c9d-a4e0-4635d7496897" />
                <img width="871" height="1559" alt="Screenshot 2026-04-16 170656" src="https://github.com/user-attachments/assets/2056a6eb-5e06-43a6-a93c-307944b0e2d5" />
                <img width="871" height="745" alt="Screenshot 2026-04-16 170810" src="https://github.com/user-attachments/assets/cbc721c6-7581-4317-a631-97c784cbf119" />
                <img width="870" height="680" alt="Screenshot 2026-04-16 170928" src="https://github.com/user-attachments/assets/8b0611ec-527b-48e4-a5d5-ba86e494fd38" />
                <p><em>- Successful.</em></p>
            <p>- H. Now, we will need to configure a default route pointing to the private WAN neighbor IP.</p>
                <img width="872" height="231" alt="Screenshot 2026-04-16 171242" src="https://github.com/user-attachments/assets/b61200ef-05dd-4b99-a5b2-bb7063b2cf5b" />
            <p>- I. Next, we'll configure the Private WAN voice quality of service.</p>
                <img width="871" height="858" alt="Screenshot 2026-04-16 171730" src="https://github.com/user-attachments/assets/3477303d-f3f7-46ad-931a-492ea96cb34d" />
                <img width="872" height="258" alt="Screenshot 2026-04-16 171825" src="https://github.com/user-attachments/assets/e95a26dd-15d8-4f09-8b88-4650ab9fb2e1" />
            <p>- J. Next, we'll configure telephony-service (max ephones, max-dn, ip source address, etc.)</p>
                <img width="868" height="337" alt="Screenshot 2026-04-16 172149" src="https://github.com/user-attachments/assets/63877c2e-3d78-4cbd-b780-cdbe54d1e13e" />
            <p>- K. Next, we'll configure Branch 1 ephone-dns.</p>
                <img width="870" height="350" alt="Screenshot 2026-04-16 172401" src="https://github.com/user-attachments/assets/f2d35d32-0152-44f8-9500-2246b1002fd5" />
            <p>- L. Now, we'll configure the PSTN access-list to the PSTN Provider for external phone service.</p>
                <p><em>- *The following access-list will allow Session Initiation Protocol, Real-time Transport Protocol and ICMP from the PSTN Provider. In addition, we have ports open that are not normally used with PSTN connections to allow the phone calls within Packet Tracer. This is because the Packet Tracer lab uses H323 signaling and ephemeral port range TCP 1024-4999. This ephemeral port range is not normally used for calls to/from the PSTN, but we will need them open for our lab to function.</em></p>
                <img width="870" height="379" alt="Screenshot 2026-04-16 172947" src="https://github.com/user-attachments/assets/bdbf4e38-c5ca-4113-804a-63bab33e5b6b" />
            <p>- M. Next, we'll configure and connect the PSTN voice interface G0/2 and apply our PSTN access-list inbound.</p>
                <img width="871" height="414" alt="Screenshot 2026-04-16 173510" src="https://github.com/user-attachments/assets/bec864ce-2d0b-4d65-bea9-02a77ca11267" />
                <img width="1155" height="879" alt="Screenshot 2026-04-16 173629" src="https://github.com/user-attachments/assets/6a696088-1778-42db-b071-c2f06fe5eabe" />
                <img width="873" height="392" alt="Screenshot 2026-04-16 173941" src="https://github.com/user-attachments/assets/29f90eb0-4b3b-4a23-a2f3-f5b40e177998" />
                <p><em>- Successful connectivity to the PSTN provider router.</em></p>
            <p>- N. Now, we'll configure internal dial-peers.</p>
                1. First, we'll configure dial peers for dialing Headquarters extensions.
                <img width="870" height="340" alt="Screenshot 2026-04-16 174353" src="https://github.com/user-attachments/assets/0f5ac575-e1b1-42e2-a4e7-e0700b703533" />
                2. Second, we'll configure dial peers for dialing Branch 2 extensions.
                <img width="870" height="271" alt="Screenshot 2026-04-16 174527" src="https://github.com/user-attachments/assets/a1ace9c5-6716-4cd2-a526-62034ec35330" />
            <p>- O. Now, we'll configure outbound dial-peers.</p>
                1. First, we'll configure dial peers for dialing 10-digit numbers:
                <img width="870" height="271" alt="Screenshot 2026-04-16 174804" src="https://github.com/user-attachments/assets/ece1306b-9b17-47f3-b5ae-2a5427e71605" />
                2. Second, we'll configure dial peers for dialing 7-digit numbers:
                <img width="873" height="266" alt="Screenshot 2026-04-16 174943" src="https://github.com/user-attachments/assets/9093dbe3-5675-4e5b-ba05-45b11df2835b" />
                3. Third, we'll configure dial peers for dialing international nunumbers:
                <img width="873" height="271" alt="Screenshot 2026-04-16 175108" src="https://github.com/user-attachments/assets/35df698a-62df-4011-9636-ae4c0930daf7" />
                4. Lastly, we'll configure dial peers for dialing 411 and 911 respectively:
                <img width="868" height="268" alt="Screenshot 2026-04-16 175250" src="https://github.com/user-attachments/assets/5585aa33-d5b3-4102-8a58-f70bc6eb1aa7" />
            <p>- P. Configure Outbound Translation Rules <em>(Lab Configuration Not Supported)</em></p>
            <p>- Q. Configure Inbound Dial-Peers <em>(Lab Configuration Not Supported)</em></p>
            <p>- R. Configure Inbound Voice Translation Rules <em>(Lab Configuration Not Supported)</em></p>
            <p>- S. Configure Voice Service VoIP <em>(Lab Configuration Not Supported)</em></p>
            <p>- T. Configure Session Initiation Protocol (SIP) <em>(Lab Configuration Not Supported)</em></p>
            <p>- U. Configure DSP Services <em>(Lab Configuration Not Supported)</em></p>
        <h3>Step 2: Install and Configure The Branch 1 Switch</h3>
            <p>- A. We'll start by racking, mounting, and powering on the branch 1 2960 switch.</p>
                <img width="1281" height="906" alt="Screenshot 2026-04-16 175802" src="https://github.com/user-attachments/assets/52b16c9b-2b4b-4f7a-ad8f-78c51d8dfa15" />
            <p>- B. Next we will do basic switch configurations (hostname, NTP, domain-name, SSH, etc).</p>
                <img width="872" height="979" alt="Screenshot 2026-04-16 180031" src="https://github.com/user-attachments/assets/939ab7dc-26f3-49e1-9910-b598ede5874d" />
            <p>- C. Next we will configure VLAN trunking protocol (VTP) transparent.</p>
                <img width="871" height="526" alt="Screenshot 2026-04-16 180520" src="https://github.com/user-attachments/assets/cdf6e515-4375-4ed3-95c7-a975f3b8549f" />
            <p>- D. Next, we'll configure MGMT vlan interface and add the voice and data vlans to the switch.</p>
                <img width="870" height="598" alt="Screenshot 2026-04-16 180841" src="https://github.com/user-attachments/assets/d1a9ed83-c8ce-4c20-9d1a-4a1eeff19b73" />
            <p>- E. *See last step*</p>
            <p>- F. Now we'll configure and connect trunks port back to the branch 1 router.</p>
                <img width="872" height="335" alt="Screenshot 2026-04-16 181154" src="https://github.com/user-attachments/assets/82b004e3-2cbc-4f32-b00a-7c9a2f64f9fd" />
                <img width="1151" height="902" alt="Screenshot 2026-04-16 181256" src="https://github.com/user-attachments/assets/1faa7292-5820-4bc6-9097-2bb8dc4625b8" />
            <p>- G. Lastly, we'll configure the access ports on the branch 1 switch.</p>
                <img width="869" height="1505" alt="Screenshot 2026-04-16 181544" src="https://github.com/user-attachments/assets/86663e80-8a33-45b4-a758-4d2716d714bf" />
                <img width="870" height="666" alt="Screenshot 2026-04-16 181634" src="https://github.com/user-attachments/assets/cbf22726-96c5-4d47-9c1b-40b024877f36" />
                <p><em>- *Now that the Branch 1 router and switch are installed, we can set up the phones, hosts & wireless!</em></p>










 





