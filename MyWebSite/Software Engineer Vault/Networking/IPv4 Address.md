---
created: 2024-02-19 10:50
aliases: 
tags: 
card link:
  - "[[Network Address Translation (NAT)]]"
source:
---
## Description
---
### Characteristics:
- 32 bits long
- Address space is 2^32

### Representations:
- bits: 00001101, 00101010, 11010101, 00101010
- dotted decimal: 0~255.0~255.0~255.0~255 (i.e. 192.1.1.2) 

### Classes:
- Class A
	- The first bits of the address must be 0: `0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx`
	- meaning that there are only the range of `0-127.0-255.0-255.0-255` lies in class A
- Class B
	- The first two bits will be 10: `10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx`
	- IP range `128-191.0-255.0-255.0-255`
- Class C
	- The first three bits will be 110: `110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx`
	- IP range `192-223.0-255.0-255.0-255`
- Class D
	- The first four bits will be 1110: `1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx`
	- IP range `224-239.0-255.0-255.0-255`
- Class E
	- The first four bits will be 1111: `1111xxx.xxxxxxxx.xxxxxxxx.xxxxxxxx`
	- IP range `240-55.0-255.0-255.0-255`

![[截圖 2024-02-19 上午11.10.50.png]]

## Reference
---





