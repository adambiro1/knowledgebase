## cheat sheet:

 
```
Group size: 128 64  32   16    8    4     2    1

Subnet:     128 192 224  240   248  252   254  255

CIDR/Subnet:/25 /26 /27  /28   /29   /30  /31  /32

``` 

 

 

### Create cheat sheet:

1. 1-128 From Right to Left
2. Subtract top from 256
3. From/32 CIDR notation Right to left

 

 

## 7 attributes of subnetting

 ```
  Network ID:

  Broadcast ID:

  First Host IP:

  Last Host IP:

  Next Network:

  Ip Addresses:

  CIDR/Subnet:
```
 

  Network ID: First IP address in each Network

  Broadcast ID: Last IP address in each Network

  First Host IP: IP address after the Network ID

  Last Host IP: IP address before the Broadcast IP

  Next Network: IP address after the Broadcast IP

  Ip Addresses: Number of IP addresses in each network

  CIDR/Subnet: Converting between CIDR/Subnet Mask

 

 

 

## Counting:

1.User given CIDR/mask to find column on Cheat Sheet

a. CIDR/Subnet Mask map to each other

b. Locate Group size:

c. Start at “.0” in relevant octet

d. increase by Group Size until you PASS target IP

2. Number BEFORE target IP is **Network ID**

3. Number AFTER target IP is the **Next Network**

4. IP address BEFORE next Network is a **Broadcast IP**

5. IP address AFTER Network ID is **First Host**

6. IP address BEFORE Broadcast IP is **Last Host**

7. Group Size is total **# of IP addresses**

*Do not forget to subtract 2 to have all usable!*

 

### Examples:

 

      10.2.2.111 /25

            .0

            .128

 

  Network ID: 10.2.2.0

  Broadcast ID: 10.2.2.127

  First Host IP: 10.2.2.1

  Last Host IP: 10.2.2.126

  Next Network: 10.2.2.128

  Ip Addresses: 
128 – 2 = 126 usable

  CIDR/Subnet: 255.255.255.128

 

 

 

#### Always pass the target number:

 

    10.2.2.20 /30                        

           .0

           .4

           .8

           .12

           .16

           .20

           .24

 

 

  Network ID: 10.2.2.20

  Broadcast ID: 10.2.2.23

  First Host IP: 10.2.2.21

  Last Host IP: 10.2.2.22

  Next Network: 10.2.2.24

  Ip Addresses: 4 – 2 = 2 usable

  CIDR/Subnet: 255.255.255.252

 

#### When passing through 255 pass it to next octet:

 
```
10.2.2.199 /26

10.2.2.0

10.2.2.64

10.2.2.128

10.2.2.192

10.2.3.0
```
 

  Network ID: 10.2.2.192

  Broadcast ID: 10.2.2.255

  First Host IP: 10.2.2.193

  Last Host IP: 10.2.2.254

  Next Network: 10.2.3.0

  Ip Addresses: 64 -2 = 62 usable

  CIDR/Subnet: 255.255.255.192

 ## Third octect:

 
```
Group size: 128 64  32   16    8    4     2    1

Subnet:     128 192 224  240   248  252   254  255

CIDR/Subnet:/25 /26 /27  /28   /29   /30  /31  /32

3rd Octet:  /17 /18 /19  /20   /21   /22  /23  /24
```
 

 
```
10.4.77.188 /19

10.4.0.0

10.4.32.0

10.4.64.0

10.4.96.0       
```
 

  Network ID: 10.4.64.0

  Broadcast ID:10.4.95.255

  First Host IP:10.4.64.1

  Last Host IP:10.4.95.254

  Next Network:10.4.96.0

 Ip Addresses: 2^13 = 8192     (32-19 = 13)     
 
 *always do* 2^(32-CIDR)

  CIDR/Subnet: 255.255.224.0

 
```
10.4.235.99. /21

10.4.224.0

10.4.232.0

10.4.240.0
```
 

 

  Network ID: 10.4.232.0

  Broadcast ID:10.4.239.255

  First Host IP:10.4.232.1

  Last Host IP:10.4.239.254

  Next Network:10.4.240.0

  Ip Addresses:  2^(32 – 21) = 2048

  CIDR/Subnet: 255.255.248.0

 

 
```
10.4.211.66 /18

10.4.0.0

10.4.64.0

10.4.128.0

10.4.192.0

10.5.0.0.0
```
 

  Network ID:10.4.192.0

  Broadcast ID:10.4.255.255

  First Host IP:10.4.192.1

  Last Host IP:10.4.255.254

  Next Network:15.5.0.0

  Ip Addresses:2^(32-18) = 16384

  CIDR/Subnet:255.255.192.0

 

 

 

## First and Second octet

 

 

 
```
Group size: 128 64  32   16    8    4     2    1

Subnet:     128 192 224  240   248  252   254  255

CIDR/Subnet:/25 /26 /27  /28   /29   /30  /31  /32

3rd Octet:  /17 /18 /19  /20   /21   /22  /23  /24

2nd Octet:  /9  /10 /11  /12   /13   /14  /15  /16

1st Octet:  /1  /2  /3   /4    /5    /6   /7   /8
```
 

## Second octet:

 
```
10.50.11.222 /12

10.0.11.222

10.16.11.222

10.32.11.222

10.48.11.222

10.64.11.222
```
 

  Network ID:10.48.0.0

  Broadcast ID:10.63.255.255

  First Host IP:10.48.0.1

  Last Host IP:10.63.255.254

  Next Network:10.64.0.0

  Ip Addresses:2^20 = 1,048,576 (32 – 12 = 20)

  CIDR/Subnet: 255.240.0.0

 

 

## First Octet:

 

 
```
10.50.111.222 /7

2.0.0.0

4.0.0.0

6.0.0.0

8.0.0.0

10.0.0.0

12.0.0.0
```
 

  Network ID:10.0.0.0

  Broadcast ID:11.255.255.255

  First Host IP:10.0.0.1

  Last Host IP:11.255.255.254

  Next Network:12.0.0.0

 Ip Addresses:2^25 = 33 554 432 (32 -7 =25)

  CIDR/Subnet:254.0.0.0

