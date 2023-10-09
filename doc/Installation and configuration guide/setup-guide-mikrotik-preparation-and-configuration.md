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