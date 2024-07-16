---
Created: 2023-08-24 10:36
alias: []
---

Source:  
Card Link: [[Linux Networking]]  
Tags: #Networking

---
## Description

How data actually comes in from socket to frameworks like converting to HTTP ?

In general, there are 4 steps:

1. Create socket by protocols
2. bind and listen the socket endpoint
3. accept the incoming protocol handshake (TCP uses [[Three Way Handshake]])
4. read, get the incoming data

```python
# this is just a pesudo code, in python we rarely use input array as buffer than output the referenced array.

# 1. this creates a socket endpoint fd, either choose TCP or UDP
listenfd = socket()

# 2. bind and listen
bind(listenfd)
listen(listenfd)
while True:
	
	# 3. Protocol handshake 
	connfd = accept(listenfd)
	while True:

		# 4. Read the input data
		buffer = []int{}
		int n = read(connfd, buffer)
		foo(buffer)
	
		if n < len(buffer): # this is the end of the data
			break
	close(connfd)
```

The main problem of the above code contains 4 system calls:

1. bind
2. listen
3. accept
4. read

System calls is a blocking operation. Therefore we need to avoid or somehow get a way with it.

Bind and listen is unavoidable and only on startup so it's ok to leave it.  
Accept is inevitable either since it is a handshake when connection comes in.

So there is the last choice, that is read(). Especially it's in the loop, where the main system calls and costs usually lies in.

![[640.gif]]![[640 (1).gif]]![[640.png]]

The above three motion demonstrates the flow when a connection from the internet comes in. This is called Blocking I/O.

To solve these problem ⇾ [[None Blocking IO]]
