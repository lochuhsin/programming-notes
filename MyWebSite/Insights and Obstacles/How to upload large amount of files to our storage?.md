---
Date: 2023-07-18 20:31
Type: Journal
Note Trait: [Decision]
---
Card Link: [[Public Clouds]], [[Pre-Signed URL]]
Tags: #Tech #Files

---
#### Introduction

This is a problem that I faces during work. We need a feature that supports user to upload files from their local computer to our system. 

The requirements are simple, maximum 100 files in once and 5 MB max per file. No need to implement resume feature.

---
#### Background

For a really simple structure of our system.
Basically we have 3 layers:
- Frontend
- Backend
- Database

Our system stores files in public cloud, and is designed to support multiple clouds storage.


---

The first thing that came to mind was to create an HTTP-based API that supports batch uploads and make changes to the content type, and all that stuff.

Well, this method sounds legit, but there are a few downsides. HTTP doesn't naturally handle massive uploads very well. It's a pain to scale, and we'd have to redo the whole upload logic for different cloud platforms.

Sure, we could try streaming or WebSockets, but here's the catch. Since we're using the backend as an intermediary service to upload files to the cloud, the files get transferred to our system first and then uploaded to the cloud. So, we end up paying double for internet traffic.

And there's another issue. It's tough for the frontend to keep track of file upload progress, like showing a progress bar.

So, here's the idea: what if we come up with a way for the frontend to upload files directly? You know, just sending basic HTTP requests, one at a time, without needing to know all the nitty-gritty details of the public cloud, e.g. composing urls.

Picture this: the frontend can easily upload a file by using a URL and the right methods. Each file would correspond to its own URL.

And that's where pre-signed URLs (so called in AWS term) come into play. Each URL comes with limited tokens that only allow uploading files to that specific address.

When it comes to the backend, we set up an API endpoint for the frontends to send filenames. In return, we provide them with the appropriate pre-signed URL. That's all there is to it—we keep all the details hidden from the frontend. What's more, we just need to handle obtaining the pre-signed URL for each public cloud. Simple as that.

Now, let's talk advantages:

1. We can save on file traffic by directly uploading files to the cloud from the frontend.
2. Authentication becomes a breeze because everything is taken care of while generating the tokens.
3. Since the API endpoint directly points to the cloud, it saves memory, and the system becomes super reliable compared to relying solely on the backend.
4. The frontend can easily add cool user experience features based on the easily managed transfer status. Think progress bars and whatnot.


I'm pretty surprise that I didn't come up this solution. Since I understand all required knowledge. Nevertheless, it is a very good experience of designing a scenario of uploading files, especially large amount of files.

Note that batch upload is a good approach, but using signed (token) url is way better if the public cloud provides such feature. 
As far as I know, AWS, Azure supports it.


