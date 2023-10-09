# Mikrotik WireGuard VPN WHMCS module

# Description

##### The module, fully installed and correctly implemented in the system, offers the following functionalities.

Module Functions:

- Auto create and deploy WireGuard VPN account
- Suspend/Unsuspend/Terminate
- Use only Mikrotik API
- Possibility to set Bandwidth speed limits
- Module supports multilingualism **(Arabic, Azerbaijani, Catalan, Chinese, Croatian, Czech, Danish, Dutch, English, Estonian, Farsi, French, German, Hebrew, Hungarian, Italian, Macedonian, Norwegian, Polish, Romanian, Russian, Spanish, Swedish, Turkish, Ukrainian)**
- Link to instructions for setting up the service in the client area.
- Link to VPN clients for setting up the service in the client area.
- In the WHMCS settings, a list of IPs is specified for use by clients.
- Ability to use both private and public IPs for clients

Available options in the admin panel:

- Create users
- Suspend users
- Terminate users
- Unsuspend users
- VPN connection status
- Text and QR code configuration types

Available options in the client panel:

- VPN connection status
- Text and QR code configuration types

- - - - - -

<p class="callout warning">WHMCS minimal version: 8 +</p>

<p class="callout warning">Mikrotik minimal version: 7 +</p>

<p class="callout info">The settings of the whmcs module when it comes to upload and download speeds register the opposite values in the mikrotik router (e.g. download speed in whmcs 1mb = upload speed in mikrotirk 1mb). This is due to the fact that from the point of view of Mikrotik, the traffic is incoming, and from the point of view of the VPN client, this is outgoing traffic.</p>

<p class="callout warning">Please be aware that to ensure proper functionality of VPN connections, it is essential for you, as an administrator, to correctly configure the Mikrotik router. This entails configuring NAT, Firewall, routing, and all the required settings for VPN to operate correctly on your router.</p>

[![image-1696798205348.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696798205348.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696798205348.png)

[![image-1696798218262.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696798218262.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696798218262.png)

<div id="bkmrk--3"><div></div></div># Changelog

##### v1.0 Anonsed 13-10-2023

First version# Installation and configuration guide



# WHMCS setup(install/update)

#####  

<p class="callout info">To install and update a module, you must perform one and the same action.</p>

<span style="font-size: 1.4em; font-weight: 400;">1. Download the latest version of the module.</span>

PHP 8.1

```Powershell
wget http://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Mikrotik-WireGuard-VPN/PUQ_WHMCS-Mikrotik-WireGuard-VPN-latest.zip
```

PHP 7.4

```Powershell
wget http://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Mikrotik-WireGuard-VPN/php74/PUQ_WHMCS-Mikrotik-WireGuard-VPN-latest.zip
```

<p class="callout info">All versions are available via link: [http://download.puqcloud.com/WHMCS/servers/PUQ\_WHMCS-Mikrotik-WireGuard-VPN/](http://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Mikrotik-WireGuard-VPN/)</p>

##### 2. Unzip the archive with the module.

```Powershell
unzip PUQ_WHMCS-Mikrotik-VPN-latest.zip 
```

##### 3. Copy and Replace "puqMikrotikWireGuardVPN" to "WHMCS\_WEB\_DIR/modules/servers/"

# Setup guide: Mikrotik preparation and configuration

#####  

<p class="callout info align-center">Note: **Enter the following commands one by one and wait for the command to complete.**</p>

##### I. Check RouterOS version

<p class="callout warning">**Make sure that the version of RouterOS is 7+**</p>

```shell
system/package/print 
```

#####  

##### II. Enabling HTTPS Create your own root CA on your router

```
/certificate
add name=LocalCA common-name=LocalCA key-usage=key-cert-sign,crl-sign
```

#####  

##### III. Sign the newly created CA certificate

```
/certificate
sign LocalCA
```

#####  

##### IV. Create a new certificate for Webfig (non-root certificate)

<p class="callout info">Note: as common-name=XXX.XXX.XXX.XXX You enter public IP adddress of the router.</p>

```
/certificate
add name=Webfig common-name=XXX.XXX.XXX.XXX
```

#####  

##### V. Sign the newly created certificate for Webfig

```
/certificate
sign Webfig ca=LocalCA 
```

#####  

##### VI. Enable SSL (*www-ssl)* and specify to use the newly created certificate for Webfig

```
/ip service
set www-ssl certificate=Webfig disabled=no
```

#####  

##### VII. Enable api-ssl and specify to use the newly created certificate for Webfig

```
 /ip service 
 set api-ssl certificate=Webfig disabled=no 
```

#####  

##### VIII. Creating a WireGuard Server

To enable the WireGuard VPN server

[![image-1696799204553.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696799204553.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696799204553.png)

# Add server (router Mikrotik) in WHMCS

#####  

##### Add a new server to the system WHMCS.

```
System Settings->Servers->Add New Server
```

- Enter the correct **Name** and **Hostname**

<p class="callout info">**Name is just for Your convenience and You can put there anything You like ie: *Mygreat mikrotik routr***</p>

<p class="callout info">**You can choose whatever hostname You want. Valid entries look similar to: vpn.mydomain.com, ourgreatvpn.mydomain.net. You can also dedicate whole domain ie: myVPNservices.com if You like. The important thing is to resolve the choosen IP address of the Mikrotik router in DNS server for Your domain.** </p>

- In the **"Assigned IP Addresses field"**, enter a list of IP addresses that will be issued to users.

[![image-1659960751104.png](https://doc.puq.info/uploads/images/gallery/2022-08/scaled-1680-/image-1659960751104.png)](https://doc.puq.info/uploads/images/gallery/2022-08/image-1659960751104.png)

- In the **Server Details** section, select the "**PUQ Mikrotik WireGuard VPN**" module and enter the correct **username** and **password** for the **Mikrotik** router.
- To check, click the **"Test connection"** button

[![image-1696799390979.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696799390979.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696799390979.png)

# Product Configuration in WHMCS

#####  

##### Add new product to WHMCS

```
System Settings->Products/Services->Create a New Product
```

In the **Module settings** section, select the **"PUQ Mikrotik WireGuard VPN"** module

[![image-1696799626331.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696799626331.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696799626331.png)

- **License key:** A pre-purchased license key for the **"PUQ Mikrotik WireGuard VPN"** module. For the module to work correctly, the key must be active
- **WireGuard interface:** A pre-created WireGuard server on a Mikrotik router, which will serve as peers for clients of this service.
- **Comment PREFIX:** The prefix that will be added to the VPN user's comment on the Mikrotik router
- **Bandwidth Download:** Download Bandwidth Limit in M/s
- **Bandwidth Upload:** Upload Bandwidth Limit M/s
- **DNS Servers:** Option in WireGuard client configuration
- **AllowedIPs:** Option in WireGuard client configuration
- **Persistent Keepalive:** Option in WireGuard client configuration
- **Link to instruction:** Link to the instruction, if filled out, it will be reflected in the client area
- **Link to VPN clients:** The URL that will be shown to the client in the client panel in order to download the VPN client

# Client Area



# Home screen

The end customer, after logging in to his own customer panel, has access to the following information and options:

- Link to the user manual (*which was defined by the administrator when setting up the service.*).
- Link to the VPN clients (*which was defined by the administrator when setting up the service.*).
- Information about available VPN protocols and statuses
- Button to download WireGuard client configuration
- VPN WireGuard clinet configuration text and QR-code

[![image-1696800149533.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696800149533.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696800149533.png)

# Admin Area



# Product Information

##### Product Information Screen

[![image-1696800612881.png](https://doc.puq.info/uploads/images/gallery/2023-10/scaled-1680-/image-1696800612881.png)](https://doc.puq.info/uploads/images/gallery/2023-10/image-1696800612881.png)

