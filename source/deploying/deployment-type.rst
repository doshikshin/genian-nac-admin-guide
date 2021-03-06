Deployment Models
=================

Genian NAC collects network information and controls the network access of devices by leveraging the following methods:

  - Layer 2 (ARP, DHCP, etc.)
  - SNMP/CLI
  - Port Mirror (SPAN)
  - 802.1x
  - Agent

Technical Considerations
------------------------

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Topic
     - Layer 2 Sensor/Enforcer
     - SNMP/CLI
     - Port Mirror (SPAN)
     - 802.1x
     - Agent
   * - **Access Control at Layer 2**
     - | Yes 
     - | Yes
     - | No
     - | Yes
     - | No
   * - **Access Control at Layer 3**
     - | RBAC
     - | Switch Port ACL
     - | RBAC
     - | Switch  Port ACL
     - | OS Firewall
   * - **Post-admission Control**
     - | ARP, DHCP
     - | VLAN/ACL/Shutdown
     - | TCP RST, ICMP unreach.
     - | CoA*
     - | OS Firewall
   * - **Additional Hardware**
     - | Network Sensor       
     - | Managed Switches
     - | Full traffic capable Device,
       | Tap Device,
       | SSL Decryption Device
     - | 802.1x Switch/AP
     - | No
   * - **Endpoint Dependency**
     - | No
     - | No
     - | No
     - | 802.1x Supplicant
     - | Agent required
   * - | **WLAN Security**
     - | Monitoring
       | (WNIC on Sensor)
     - | Monitoring
       | (SNMP with Controller)
     - | No
     - | Monitoring / Control
       | (WPA2-Enterprise)
     - | Monitoring / Control
       | (SSID Whitelist)
   * - **Layer 2 Security**
     - | Detect MAC Spoofing,
       | Detect Rogue DHCP,
       | Managing IP Conflict
     - | No
     - | No
     - | No
     - | No

*CoA\*: Change of Authorization, RFC 5176 - Dynamic Authorization Extensions to RADIUS*

Management Considerations
-------------------------

.. list-table::
   :widths: auto
   :header-rows: 1

   * - Topic
     - Layer 2 Sensor/Enforcer
     - SNMP/CLI
     - Port Mirror (SPAN)
     - 802.1x
     - Agent
   * - **Network Config Change**
     - | Trunk port (optional)
     - | Switch Config,
       | VLAN/ACL
     - | Tap Device,
       | SPAN Port
     - | Switch Config,
       | VLAN/ACL,
       | Endpoint Config
     - | No
   * - **Compatibility Issue**
     - | No
     - | Vendor-dependent
       | SNMP MIB/CLI
     - | No
     - | RADIUS Vendor Attribute,
       | non-802.1x capable Device
       | (*Poor wired device support*)
     - | OS Type/Version
   * - **Easy of Deployment**
     - | Easy
     - | Difficult
     - | Intermediate
     - | Very Difficult
     - | Intermediate
   * - | **Phased Deployment**
       | (Discover First, Control Later)
     - | Yes
     - | Yes
     - | Yes
     - | Must be controlled from
       | the start of deployment
     - | Yes
   * - **Single point of Failure**
     - | No
     - | Yes
     - | Yes
     - | Yes
     - | No
   * - **Vendor Lock-in**
     - | No
     - | Intermediate
     - | No
     - | High
     - | Intermediate
   * - **Recommended for**
     - | Essential Discovery
       | and Control
     - | Extended information
       | and port control
     - | 
     - | Wireless network
     - | Extended information
       | and enforce compliance

Policy Server Deployment Models
-------------------------------

On-Premises
'''''''''''

**Policy Server** and **Network Sensor** can be deployed one of two ways

   -  Policy Server/Network Sensor combined
   -  Policy Server and Network Sensor separated
   
The switch port can be a standard connection or can be a trunked port for up to 128 VLANs. If your location has more than 128 VLANs then a second Network Sensor would be required
(*If you have 2 Network Sensors on the same network or overlapping networks in an 802.1q environment you will have duplicate nodes. There is no harm in having duplicated nodes, it is just something to be aware of.*)

Policy Server and Network Sensor Combined

.. image:: /images/Deploying-PolicyServer-NetworkSensor-Combined.png
   :width: 600px

Policy Server and Network Sensor Separated

.. image:: /images/Deploying-PolicyServer-NetworkSensor.png
   :width: 600px

Cloud-Managed
'''''''''''''

**Policy Server** can be deployed in the Cloud, while **Network Sensors** can be deployed by connecting them to an Edge Switch at your Remote Site locations.  The Edge Switch ports can be a standard connection or can be trunked ports for up to 128 VLANs. If your location has more then 128 VLANs then a second **Network Sensor** would be required

.. image:: /images/Deploying-PolicyServer-NetworkSensor-Cloud.png
   :width: 600px

