# **Network Configuration and Access List**

## **Interface Configuration Router 3 **
```
interface FastEthernet1/0
 description LAN interface (60.0 network icin) 53, 80 ve 443'e giden izinler ve yasaklar
 ip address 192.168.60.1 255.255.255.0
 ip access-group WEB-FILTER in
```

```
ip access-list extended WEB-FILTER
 remark -------------------------
 remark ACL: WEB - FILTER
 remark Purpose: 60.0 Networkundeki istemcilerin 192.168.10.5 HTTP ve DNS kontrolu
 remark ------------------------
```
```
 remark -----------------------
 remark Routing Trafic
 permit ospf any any
 remark ----------------------
``` 
 
 ** remark 60.10-11-12/24 Network**
```
 remark Sadece 60.10-11-12 IP'leri HTTP ve DNS'e erisebilir
 permit tcp host 192.168.60.10 host 192.168.10.5 eq www
 permit tcp host 192.168.60.10 host 192.168.10.5 eq domain
 permit udp host 192.168.60.10 host 192.168.10.5 eq domain
```
``` 
 remark ---- 60.11 ----
 permit tcp host 192.168.60.11 host 192.168.10.5 eq www
 permit tcp host 192.168.60.11 host 192.168.10.5 eq domain
 permit udp host 192.168.60.11 host 192.168.10.5 eq domain
```
``` 
 remark ---- 60.12 ----
 permit tcp host 192.168.60.12 host 192.168.10.5 eq www
 permit tcp host 192.168.60.12 host 192.168.10.5 eq domain
 permit udp host 192.168.60.12 host 192.168.10.5 eq domain
``` 
```
 remark ---- 60.10-11-12 IP'leri HTTPS'e erişemez ----
 deny   tcp host 192.168.60.10 host 192.168.10.5 eq 443
 deny   tcp host 192.168.60.11 host 192.168.10.5 eq 443
 deny   tcp host 192.168.60.12 host 192.168.10.5 eq 443
```
``` 
 remark ------------------------------
 remark Local Policy
 remark Yukaridaki kurallara uymayan diger tum istemcileri icin 10.5 erisimini engelle
 deny   ip any host 192.168.10.5
 remark Diger Networklere giden trafige izin ver
 permit ip any any
 remark ------------------------------
```