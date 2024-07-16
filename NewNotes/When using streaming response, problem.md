---
Created: 2023-10-31 09:52
URL:
---

Card Links:  
Tags:

---
## Description:

When using streaming response, meaning the data is generated instead of send in one packet. The possible problem is that, the status code (i.e 200) is already send even though the data is corrupted later on. Their for the client must carefully handle the interrupt payload if the connection is broken suddenly, or the server should send a data (json) to show data is corrupted.

---
## References: