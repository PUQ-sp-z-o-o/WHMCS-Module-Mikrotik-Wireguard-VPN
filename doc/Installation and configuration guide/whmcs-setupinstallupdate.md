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