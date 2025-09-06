\## R0



```

interface GigabitEthernet0/0
ip address 10.0.10.2 255.255.255.252

```

```

interface GigabitEthernet0/1
ip address 192.168.20.1 255.255.255.0

```

```

router ospf 1
router-id 2.2.2.2
network 10.0.10.0 0.0.0.3 area 0
network 192.168.20.0 0.0.0.255 area 1

```

---



\## R1



```

interface GigabitEthernet0/0
ip address 10.0.10.1 255.255.255.252

```

```

interface GigabitEthernet0/1
ip address 192.168.10.1 255.255.255.0

```

```

interface Serial0/0/0
ip address 10.0.30.1 255.255.255.252
clock rate 2000000

```

```

router ospf 1
router-id 1.1.1.1
network 10.0.10.0 0.0.0.3 area 0
network 10.0.30.0 0.0.0.3 area 0
network 192.168.10.0 0.0.0.255 area 0

```

---



\## R2



```

interface GigabitEthernet0/0
ip address 10.0.40.1 255.255.255.252

```

```

interface GigabitEthernet0/1
ip address 192.168.30.1 255.255.255.0

```

```

interface Serial0/0/0
ip address 10.0.30.2 255.255.255.252

```

```

router ospf 1
router-id 3.3.3.3
network 10.0.30.0 0.0.0.3 area 0
network 10.0.40.0 0.0.0.3 area 2
network 192.168.30.0 0.0.0.255 area 2
area 2 virtual-link 4.4.4.4

```

---



\## R3



```
interface GigabitEthernet0/0
ip address 10.0.40.2 255.255.255.252

```

```

interface GigabitEthernet0/1
ip address 192.168.40.1 255.255.255.0

```

```

router ospf 1
router-id 4.4.4.4
network 10.0.40.0 0.0.0.3 area 2
network 192.168.40.0 0.0.0.255 area 3
area 2 virtual-link 3.3.3.3

```

---

