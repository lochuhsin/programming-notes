---
Date: 2023-07-19 21:14
Type: Journal
Note Trait: Tech
---
Card Link: [[System Design]], [[WebSocket]]
Tags:

---
## Introduction
This is a system design related problem we encountered recently. Essentially, we are discussing how to integrate a new feature server into our system. The discussing process is truly fascinating. Numerous lot of designing details were brought up. I believe it is highly valuable to document the entire exchange.


## Background

Now, let us start with some compact version of our system.
1. Frontend
2. Backend
3. Databases
4. .... etc, unnecessary components

To request the feature server, the caller should send the following information.
- 2 image files / url, (5MB max)
- embedding file / url (5MB max)
- and some basic parameters.
- The response time for each request is around 0.5 seconds.
- the response data is used for frontend to draw something on the canvas.
- Heavy calculation, therefore it's not possible for consuming burst requests.

Use case:
When the user clicks on an image showing in the browser and added a point to it, the anticipate an immediate response with the object segmented. It's natural to expect a slight waiting time of 1 to 2 seconds, but not more than that. Furthermore, the user probably interact on multiple points and images, though the limit remains within 10 instances in this particular case


## Insights and Lessons Learned
The easiest way of solving problem is obviously by using basic http requests everywhere. The frontend sends the image_id or url to backend, during this request backend sends http requests to feature server. Then the feature server response backend process the response and send back to frontend.

So, what could go wrong here ?
First of all, this request across two layers, backend and feature server. Moreover it involves sending images and files.
If the users keeps clicking the image, the feature server will obviously breakdown. The image files (either backend or server) will consumes lots of internet traffic and the response time will be extremely slow.

For immediately response and frequently request, we decided to use WebSocket to communicate with frontend. The reason is, user burst requests could be reduced, backend can build a queue or a request buffer to handle these request. Then using http sends these information to feature server.

#### Pros:
- backend could handle requests more easily
- no need to handle burst request
- the connection status between backend and server still stays simple.


#### Cons:
- Since there might be a lot of users using the same feature, backend need the capability to handle concurrency very well. e.g lots of WebSockets in the same time.


## Conclusion:
I believe this is a compelling use case for integrating WebSocket. After detailed discussion meeting, I have a deeper understanding of choosing different api protocols.


Medium:
https://albert-lo.medium.com/adding-new-feature-server-to-our-system-5c16d3bab8d7

