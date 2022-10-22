---
layout: post
title:  "TryHackMe OhSint Room Writeup"
date: 2022-10-19
categories: ctf osint
---

This is a writeup for the TryHackMe room "OhSint" found here. This is a beginner-level OSINT CTF but is still a fun one to work through. Let's get started!

**The Room** <br>
In this room, we are given this picture:

<img src="/images/ohsint/WindowsXP.jpg" alt="WindowsXP" width=50% height=50%>

And told to find the following information:

1. What is this user's avatar of?
2. What city is this person in?
3. What's the SSID of the WAP he connected to?
4. What is his personal email address?
5. What site did you find his email address on?
6. Where has he gone on holiday?
7. What is this person's password?

**The Writeup**

Seems complicated at first glance, but once we get into it, there is a lot of information easily available. The first thing to do here is download the file and look at the metadata. There are a couple of ways to do this, but I used metadata2go.com and analysed the file using that. We get this metadata:

<img src="/images/ohsint/ohsintmetadata.png" alt="Metadata Of File" width=50% height=50%>

Another way we can do this if you have a Linux system is to run the command exiftool on the file.

<img src="/images/ohsint/ohsintexif.png" alt="Metadata Of File Using Exiftool" width=50% height=50%>

As you can see we get the same information from both methods. The important information here is the copyright - "OWoodflint", the name of the person who owns the image. If we google this we will get some interesting results: a twitter page, a blog, and a Github repository.

<img src="/images/ohsint/searchresults.png" alt="Search Results" width=50% height=50%>

Let's take a look at the twitter page first. This will give us the answer to the first question - "What is this user's avatar of?". It's a cat!

<img src="/images/ohsint/twitter.png" alt="Twitter Page" width=50% height=50%>

We can also get some interesting information here - they have (stupidly) posted their BSSID on their twitter page. We can use this to work out their location! Go to wigle.net (you will need to make an account for this) and perform a Basic Search using the BSSID. A result called UnileverWifi will appear, double-click it and the map will drop you right on the city - they are in London!

<img src="/images/ohsint/wigle.png" alt="Wigle Results" width=75% height=75%>

This search gives us the answer to two questions. The city - London. The SSID - UnileverWifi. <br>
Now we can move on from the Twitter page. Let's look at the Github repository next.

<img src="/images/ohsint/github.png" alt="Github Repo" width=50% height=50%>

Straightaway we have our next two answers, the personal email address and we website we found it on!<br>
Now we can move to the blog for the final two questions.

<img src="/images/ohsint/blog.png" alt="Wordpress Blog" width=50% height=50%>

We can immediately see that Oliver has been very open about his holidays, and he is in New York!<br>
Now we only have one task left, to find Oliver's password. Normally to find passwords we would need to do some hacking or password cracking, but this is an OSINT room, so we can rule those methods out. We can take a look around the blog, but we won't find much. Let's take a look at the source code of the main blog page. <br>

There is a lot to look through, but when we scroll down to the main code for the blog page, we can spot something looking a little out of place.

<img src="/images/ohsint/pass1.png" alt="Password Hidden in Source Code" width=50% height=50%>

This is our password! Reading the code, we can see it is in the main body of the blog page, just in white. So if we go back and highlight that area, we can see it sneakily hidden in (almost) plain sight!

<img src="/images/ohsint/pass2.png" alt="Password Hidden on Blog Page" width=50% height=50%>

That brings us to the end of this room. Fairly easy once you get the search results but I still had fun with it!






