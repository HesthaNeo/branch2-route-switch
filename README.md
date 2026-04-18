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
                4. Lastly for this step, we will proceed with creating the map that will be applied to the VPN-ONLY internet interface.
                <img width="860" height="725" alt="Screenshot 2026-04-18 180730" src="https://github.com/user-attachments/assets/e9373864-04a3-4bce-845f-952d427faca8" />
            <p>- G. Next, we'll configure an access control list that only allows traffic from the HQ IPSec VPN tunnel.</p>
                <img width="871" height="386" alt="Screenshot 2026-04-18 181320" src="https://github.com/user-attachments/assets/9e95d3cf-7a28-4f01-9698-272b7d247d96" />
            <p>- H. Now, we will configure and connect the VPN-ONLY internet connection for the site-to-site VPN to HQ, which in this case will be Internet interface G0/1.</p>
                <img width="874" height="429" alt="Screenshot 2026-04-18 182421" src="https://github.com/user-attachments/assets/d349755f-5416-4b9c-93d7-ae33149f6e65" />
                <img width="1186" height="934" alt="Screenshot 2026-04-18 182613" src="https://github.com/user-attachments/assets/1f60ec7f-c9bc-47ef-92c3-5ff7d1388b07" />
                <p><em>- We will test connectivity. We will first remove the ACL to temporarily allow test pings back in.</em></p>
                <img width="870" height="496" alt="Screenshot 2026-04-18 182935" src="https://github.com/user-attachments/assets/ab4e2947-c006-45b1-941f-58df3a4aed3f" />
                <p><em>- Successful.</em></p>
            <p>- I. Next, we'll add static routes for the default route and VPN endpoint.</p>
                <img width="873" height="241" alt="Screenshot 2026-04-18 183238" src="https://github.com/user-attachments/assets/0865b987-d315-481f-bfeb-6eb0d91b10b2" />
                <p><em>- Successful.</em></p>
                

                

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










 





