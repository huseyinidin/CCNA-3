# **Network Configuration and Access List**

## **Interface Configuration Router 3 **
```
interface FastEthernet1/1
 description 30.10-12 cikamaz sadece 30.15-17 cikabilir
 ip address 192.168.30.1 255.255.255.0
 ip access-group WEB-FILTER in
```

```
ip access-list extended WEB-FILTER
 remark -------------------------
 remark ACL: ICMP, DNS and WEB - FILTER
 remark Purpose: 30.0 Networkundeki istemcilerin 192.168.10.5  ICMP, DNS ve HTTP kontrolu
 remark ------------------------
```
```
 remark -----------------------
 remark Routing Trafic
 permit ospf any any
 remark ----------------------
``` 
 **remark ---- 30.10, 30.11, 30.12 ----**

``` 
 remark 30.10, 30.11 ve 30.12 istemcilerinin ICMP, DNS ve HTTP  erisimi tamamen yasak
 deny   icmp 192.168.30.8 0.0.0.2 host 192.168.10.5
 deny   udp 192.168.30.8 0.0.0.2 host 192.168.10.5 eq domain
 deny   tcp 192.168.30.8 0.0.0.2 host 192.168.10.5 eq domain
 deny   tcp 192.168.30.8 0.0.0.2 host 192.168.10.5 eq www
 deny   tcp 192.168.30.8 0.0.0.2 host 192.168.10.5 eq 443
 ```
 **remark ---- 30.15, 30.16, 30.17 ----**
```
 remark 30.15, 16-17 istemcileri sadece ICMP, DNS ve HTTPS (443) erisimi yapabilir, HTTP (80) kapali
 remark ---- permit ----
 remark ---- 30.15 ----
 permit icmp host 192.168.30.15 host 192.168.10.5
 permit udp host 192.168.30.15 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.15 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.15 host 192.168.10.5 eq 443
```
``` 
 remark ---- 30.16 ----
 permit icmp host 192.168.30.16 host 192.168.10.5
 permit udp host 192.168.30.16 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.16 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.16 host 192.168.10.5 eq 443
``` 
``` 
 remark ---- 30.17 ----
 permit icmp host 192.168.30.17 host 192.168.10.5
 permit udp host 192.168.30.17 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.17 host 192.168.10.5 eq domain
 permit tcp host 192.168.30.17 host 192.168.10.5 eq 443
 ``` 
 ```
 remark ---- Deny ----
 deny   tcp 192.168.30.13 0.0.0.2 host 192.168.10.5 eq www
 deny   tcp 192.168.30.16 0.0.0.2 host 192.168.10.5 eq www
 deny   tcp 192.168.30.17 0.0.0.2 host 192.168.10.5 eq www
```
```
 remark ------------------------------
 remark Local Policy
 remark Yukaridaki kurallara uymayan diger tum istemcileri icin 10.5 erisimini engelle
 deny   ip any host 192.168.10.5
 remark Diger Networklere giden
 permit ip any any
 remark -----------------------------

```