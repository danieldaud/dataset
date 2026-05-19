# Network Design and Implementation















Section One: Research

### Introduction

A robust network infrastructure stands as a pivotal element for any thriving organization seeking success in today's competitive market. It serves as the fundamental communication conduit connecting the business with its clients. In the contemporary landscape, the efficacy of your IT infrastructure plays a decisive role in positioning your business ahead of competitors. The pervasive influence of Information Technology has reshaped business operations, elevating performance, enhancing flexibility, fostering digital awareness, automating services, and ushering in numerous other transformative benefits.

Recognizing the transformative impact of IT, it becomes imperative to accord due diligence to the planning, design, implementation, and testing phases of network infrastructure development. Only by adhering to the best practices in network design can an organization ensure the seamless deployment and optimal utilization of its network resources. In essence, the careful consideration of these aspects lays the foundation for a robust and future-ready network infrastructure, essential for sustaining competitiveness and achieving operational excellence in today's dynamic business environment.







































Redundancy and Scalability in the Network

Ensuring both availability and reliability during the design and implementation of the network is crucial to prevent a single point of failure. For instance, the access switches are connected to two multilayer switches, allowing the second one to take over communication in the event of the primary core switch being down. Redundancy in networking involves employing multiple links so that if one fails, another can seamlessly take over (Mas-Machuca, 2016). In this network system, redundancy is achieved through the use of etherchannel, multiple core switches/routers/firewalls, and numerous links between devices, as illustrated in the topology.

Future expansion is a vital consideration in design, and the network is crafted to support it. The design allows for the addition of more modules without compromising network performance.

Security in the Company Network

Security is paramount in any network, and the telephony company network incorporates several security measures. Access is restricted to authorized users through password protection (for line console, VTY, and privilege EXEC), utilizing SSH for remote login. The Virtual Local Area Network (VLAN) is implemented for segmentation and added security. A site-to-site IPsec VPN ensures a secure tunnel for communication between branches and headquarters. Additionally, the Cisco ASA firewall is deployed to establish distinct security levels between inside and outside networks, permitting only the inside network to initiate communication. Any traffic originating from the outside to the inside network is denied.

















Section Two: Design

Proposed Network Design and Implementation

A comprehensive study conducted by Hamid (2021) underscores the reality that deeming any network as perfect and error-free is highly improbable unless subjected to rigorous expert analysis and evaluation, or scrutinized for vulnerabilities through potential attacker penetration capabilities. In the context of a specific case study, consider DFS (hypothetical organization) with four integral departments—Human Resources (HR), Information Technology (IT), Customer Service (CS), and Marketing (MK)—all housed within its main headquarters.

In a strategic move, the senior management of DFS has made the decision to establish an independent network infrastructure. This infrastructure encompasses a Local Area Network (LAN), a Wide Area Network (WAN), and an external Server-Side location connected through appropriate WAN technology. The emphasis is on ensuring secure communication, particularly prioritizing the exchange of information between the HR department and the external server-side site. This server-side location is slated to host critical servers, including DNS, WEB, and EMAIL, solidifying the organization's commitment to a robust and secure network framework.

The Layered Hierarchical Network Design

Danilo (2018) emphasizes the significance of layered network design, presenting three key layers—core, distribution, and access. These layers are strategically crafted to enhance performance, bolster security, and simplify network maintenance. Each layer serves distinct functions within the architecture, collectively working towards specific network objectives. This approach offers valuable insights into constructing a network that is not only high-performing but also scalable, secure, and easily manageable, as articulated by Sinket (2019). Please find attached the proposed network design for your consideration.



Subnetting (Design IP Addressing and Allocation)

In the meticulous process of IP address allocation, special attention was given to devising a systematic approach for addressing between routers, multilayer switches, and individual departments through the implementation of subnetting. This detailed allocation strategy ensures efficient communication and seamless data transfer between routers, multilayer switches, and different departments. The subnetting methodology applied is instrumental in optimizing network performance and resource utilization.

The following table delineates the structured IP addressing scheme employed for these purposes:

Between the Routers, Multilayer switches

HQ Departments

Server-Side Site



### d.  Basic Device Configurations

In configuring our network, a series of fundamental device settings were meticulously established through the Command Line Interface (CLI). These configurations encompassed essential parameters such as hostnames, banner messages, line console passwords, privilege mode passwords, line VTY passwords with SSH, usernames and passwords, domain names, the disabling of IP domain lookup, setting exec-timeout, enabling logging synchronous, and culminating with the encryption of all configured passwords.

Each of these configurations serves a crucial role in fortifying device entry security and imbuing each device with additional important features, as illustrated in the attached figure;

Sample Basic Configuration Commands



Basic Configuration Results

Using the following commands in privilege-exec mode: show start or show startup-config



VLAN Configuration, VLAN Trunking 802.1Q, Inter-VLAN Routing

VLANs

To enhance security and streamline maintenance, a distinctive VLAN has been assigned to each department within the HQ network, with each VLAN corresponding to a unique subnet. By default, devices residing in separate VLANs are isolated from one another, necessitating the implementation of inter-VLAN communication to enable seamless interaction. Below is an illustrative example of VLAN configuration and the associated VLAN database within the network switches.

### a. Sample VLAN Configuration Commands



### b. VLAN Configuration Results

Using the following commands in privilege-exec mode: show start or show vlan brief



VLAN Trunking (802.1Q)

To enable VLAN traffic exchange among switches within the network, we implemented trunk links as a means of facilitating seamless communication. Presented below are examples showcasing the configuration for VLAN trunking in the network switches. This configuration plays a pivotal role in ensuring efficient data flow and interconnectivity between switches, enhancing the overall performance and cohesion of the network.

Sample Trunking Configuration Commands



Trunking Configuration Results

Using the following commands in privilege-exec mode: show interfaces trunk











Inter-VLAN Routing

By default, communication between devices in different VLANs is restricted unless inter-VLAN routing is implemented. In our configuration process, we opted for switch virtual interface (SVI) as the protocol for inter-VLAN routing. This involves creating VLAN interfaces and assigning them specific IP addresses. Below are examples providing insight into the inter-VLAN routing configuration implemented in the routers. This approach ensures effective communication across VLANs, fostering a well-connected and interoperable network environment.

Sample Inter-VLAN Configuration Commands



Inter-VLAN Configuration Results

Using the following commands in privilege-exec mode: show start





EtherChannel or Link Aggregation Configuration

The link aggregation technique serves as a mechanism wherein multiple switch links amalgamate into a singular logical channel, functioning as a unified conduit for forwarding data. According to Cisco, up to 8 links can be aggregated to form this cohesive logical link. This approach not only enables the efficient distribution of traffic across the links, promoting load sharing, but also establishes redundancy in the event of one or more links in the channel experiencing failure.

Implementing link aggregation technology ensures optimal bandwidth utilization, eliminates the risk of loops, and introduces redundancy within the network. In our topology, we adopted the Link Aggregation Control Protocol (LACP) to establish the EtherChannel, as depicted below. This strategic use of technology further fortifies network resilience and performance.

Sample LACP Configuration Commands



LACP Configuration Results

Using the following commands in privilege-exec mode: show etherchannel port-channel



Host-Standby Router Protocol Configuration (HSRP)

For optimizing load sharing and ensuring failover capabilities within the network, the Hot Standby Router Protocol (HSRP) emerges as a crucial protocol. It plays a pivotal role in maintaining network availability in scenarios where a node is either down or experiencing faults. In our network configuration, HSRP was strategically implemented in conjunction with Switched Virtual Interface (SVI) interfaces to effectively load balance traffic traversing the SVIs.

In this setup, both multilayer switches function as both active and standby nodes for the SVIs. If one SVI encounters a disruption, the corresponding SVI on the alternate switch is activated. Similarly, in the event of one multilayer switch facing an issue, all network traffic is seamlessly routed through the operational switch. This robust configuration ensures uninterrupted network functionality, bolstering reliability and minimizing downtime, as illustrated below;

Sample HSRP Configuration Commands



HSRP Configuration Results

Using the following commands in privilege-exec mode: show standby brief



DHCP Server, DNS Server, Web Server, Email Server

DHCP Server

In the HQ network, dynamic allocation of IPv4 addresses for all host devices is facilitated through a dedicated DHCP server located at the server-side site. This DHCP server plays a pivotal role in automating the assignment of IPv4 addresses, ensuring seamless connectivity for all devices within the network.

The diagrams below provide insights into the DHCP server configurations and serve as tangible evidence showcasing the automatic assignment of IPv4 addresses. This approach streamlines network management, eliminates manual address assignment, and contributes to the efficient and automated operation of the HQ network, as depicted in the illustrations.

Sample DHCP Configurations



DHCP Configuration Results



DNS Server

In our network setup, domain name resolution is facilitated by the DNS server, which plays a critical role in translating human-readable domain names into IP addresses. The configuration details of the DNS server, along with tangible evidence showcasing successful resolution, are outlined below.

Sample DNS Configuration





DNS Configuration Results

This robust DNS server configuration ensures efficient and accurate resolution of domain names within the network, contributing to seamless communication and accessibility of resources.





Web Server

The web server within our network has been meticulously configured, tailored to our specific requirements with additional HTML files. This strategic setup ensures that all hosts within the network can seamlessly access the designated web pages. Below, we present samples of the HTML configuration procedures and the resulting outcomes on the host devices.

Sample Web Configuration



Web Configuration Results

This configuration not only ensures the accessibility of web pages by all hosts but also allows for the seamless customization of content to meet specific organizational needs.



Email Sever

In order to establish the capability for sending and receiving emails within our network, the email server has undergone meticulous configuration to support both SMTP (Simple Mail Transfer Protocol) for sending emails and POP3 (Post Office Protocol version 3) for receiving emails. The ensuing samples illustrate the configuration steps and showcase the outcomes on the host devices.

Sample Email Configuration



Email Configuration Results

This comprehensive configuration not only ensures efficient email communication within the network but also provides a secure and streamlined environment for both sending and receiving emails.



Dynamic Routing Protocol Configuration- OSPF

To facilitate efficient routing and communication within our network, OSPF (Open Shortest Path First) was employed as the designated routing protocol. The ensuing segment outlines the key OSPF configuration commands and presents the corresponding output from the router.

This configuration empowers OSPF to dynamically exchange routing information and compute the optimal paths, ensuring efficient communication throughout the network.

Sample OSPF Configuration



OSPF Configuration Results

Using the following commands in privilege-exec mode: show IP OSPF neighbor



Section Three: Evaluation

Access Control, User Privileges, and IPsec VPN

User Privileges

Security stands as a cornerstone in the design and implementation of any network. In our network infrastructure, stringent security measures have been implemented to safeguard user privileges, focusing on both line console user and privileged exec mode. The meticulous execution of security protocols includes password protection, ensuring encryption for heightened protection.

Line Console User Privileges: The console port, utilized for local system access using a console terminal, has been configured for enhanced security. Although the console port does not inherently require a password for administrative access, we have instituted a line-level password for added protection. Users' access to the line console and privileged exec mode has been carefully controlled. Passwords have been implemented for both line console and privileged exec modes. Passwords are encrypted to fortify their security.

Enable Password for Privilege Mode: The enable password has been employed to secure privilege mode, ensuring controlled access. To prevent the display of passwords in plain text, the service password-encryption command has been implemented.







Access Control Lists

In accordance with Pluralsight (2019), Access Control Lists (ACLs) serve as network filters employed by routers and certain switches to manage and control the flow of data into and out of network interfaces. When configured on an interface, ACLs meticulously scrutinize data passing through, comparing it against specified criteria, and subsequently deciding whether to permit or deny the data flow. In our network design, ACLs have been strategically leveraged to bolster security by filtering traffic based on predefined rules.

Extended ACL: To fortify the security of communication between the HQ network and the Server-side network, the first access control list (Extended ACL) was implemented. This was complemented by the establishment of a site-to-site VPN connection on both the HQ and Server-side routers. This measure ensures that only authorized traffic is allowed between the designated networks, enhancing data confidentiality and integrity.







Standard ACL: The second ACL was deployed specifically on the line VTY interfaces of the HQ-router. This Standard ACL was configured to exclusively permit SSH access to the router, ensuring that only members of the IT department possess the authorization to establish secure shell connections. This meticulous control over remote access contributes to a more secure and controlled network environment.





Testing ACL for Remote SSH Access



IPsec VPN

In alignment with GeeksforGeeks (2020), Virtual Private Networks (VPNs) play a pivotal role in providing secure and private access to a network over the Internet. This technology establishes an encrypted connection, commonly referred to as a VPN tunnel, through which all Internet traffic and communications are securely transmitted. In our network architecture, the implementation of IPsec VPN (Internet Protocol Security) serves as a robust solution for securing internet communication over the IP network. IPsec enhances security by validating sessions and encrypting all data packets exchanged during communication.

Key Aspects of IPsec VPN Implementation

Secure Communication: IPsec VPN creates a secure channel, commonly known as a tunnel, ensuring the confidentiality and integrity of data transmitted over the network.

Verification and Encryption: IPsec verifies the authenticity of communication sessions and encrypts data packets, providing a comprehensive security layer for network traffic.

Site-to-Site VPN Implementation

In our network, a site-to-site VPN has been strategically implemented between the HQ and server-side routers to establish secure communication channels. This ensures that all traffic flowing between the HQ and Server-side networks is encrypted, mitigating the risk of interception by potential sniffers or eavesdroppers.

Security Measures with ACLs

To enhance security, the implemented Access Control List (ACL) specifies rules allowing only the HQ subnets to engage in secure communication with the servers. This meticulous control over network traffic contributes to the overall security posture, preventing unauthorized access and ensuring that only designated entities can communicate securely.



## 4.0 Section Four: Ethical Consideration

In conclusion, the proposed DFS network aligns with fundamental information security principles, particularly the CIA triad—Confidentiality, Integrity, and Availability.

Confidentiality- The implementation of Virtual Local Area Networks (VLANs), SSH for remote login, and the use of Virtual Private Network (VPN) technologies such as IPsec contribute significantly to maintaining confidentiality. VLANs and VPNs ensure that sensitive data is segmented and transmitted securely over encrypted channels, protecting it from unauthorized access.

Integrity- The redundancy and scalability features of the network enhance data integrity. Redundancy mechanisms, including multiple core switches and links, reduce the risk of data corruption or loss in case of network failures. Scalability allows for the seamless addition of resources without compromising the integrity of existing data.

Availability- Redundancy and scalability are key components ensuring high availability. The multiple core switches and EtherChannel configurations provide failover capabilities, guaranteeing continuous network availability. The implementation of IPsec VPN also plays a crucial role in ensuring the availability of secure communication channels between different branches and headquarters.

The proposed network design, by adhering to these information security principles, fortifies the overall company network and security systems. It establishes a robust, reliable, high-performing, and secure network infrastructure that positions the company for greater success in the market. Therefore, based on our findings, we strongly recommend the company proceed with the implementation of the proposed network to enhance its overall information security posture and achieve optimal network performance.











## 5.0. References

Azzedin, F. & Maheswaran, M. (2022). “Towards Trust-Aware Resource Management”, Proceedings of the 2nd IEEE/ACM International Symposium on Cluster Computing and the Grid (CCGrid’02).

Bian, L., 2023. Design of computer network security defense system based on artificial intelligence and neural network. Wireless Personal Communications, pp.1-20.

Griner, C., Schmid, S. and Avin, C., 2022. CacheNet: Leveraging the principle of locality in reconfigurable network design. Computer Networks, 204, p.108648.

Radosavovic, I., Kosaraju, R.P., Girshick, R., He, K. and Dollár, P., 2020. Designing network design spaces. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 10428-10436).

Gunduz, M.Z. and Das, R., 2020. Cyber-security on smart grid: Threats and potential solutions. Computer networks, 169, p.107094.

Xu, W., Zhang, J., Kim, J.Y., Huang, W., Kanhere, S.S., Jha, S.K. and Hu, W., 2019. The design, implementation, and deployment of a smart lighting system for smart buildings. IEEE Internet of Things Journal, 6(4), pp.7266-7281.

Yulianaa, D. and Mogia, I.K.A., 2020. Computer Network Design Using PPDIOO Method With Case Study of SMA Negeri 1 Kunir. Jurnal Elektronik Ilmu Komputer Udayana p-ISSN, 2301, p.5373.

Hamid G. (2021). Scalable Synchro phasors Communication Network Design and Implementation for Real-Time Distributed Generation Grid. IEEE Transactions on smart grid journal pp4-11.

Vestin, J., Kassler, A. & Akerberg, J. (2019). “Resilient software defined networking for industrial control networks.” Conference on Information, Communications and Signal Processing (ICICS). IEEE, pp. 1–5.

Danilo, C. (2020). Fast Packet Processing: A Survey. IEEE Communications Surveys & Tutorials.

Sinket (2019). Hierarchical Network Design. Retrieved from; https://www.ques10.com/p/50374/network-hierarchy/

Pluralsight (2019). Access Control Lists. Obtained from; https://www.pluralsight.com/blog/it-ops/access-control-list-concepts

Dusan Hrabec et al.,2020. Circular economy implementation in waste management network design problem: a case study. Central European journal of Operation research pp12-78.

Alharbi, R. & Aspinall, D. (2018). An IoT analysis framework: An investigation of IoT smart cameras' vulnerabilities. IoT 2018.

Ullah, S. et al. (2019). Secure smart cameras by aggregate-signcryption with decryption fairness for multi-receiver IoT applications. Sensors, 19(2), p.327. Retrieved from; https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6359113/

SecureUD (2020). Network Security. Retrieved from; https://www.secureus.app/