---
layout: post
title:  "TryHackMe OhSint Room Writeup"
date: 2022-10-19
categories: ctf osint
---

This is a writeup for the TryHackMe room "OhSint" found here. This is a beginner-level OSINT CTF but is still a fun one to work through. Let's get started!

**The Room** <br>
In this room, we are given this picture:

![WindowsXP](/_site/assets/ohsint/WindowsXP.jpg)

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

![MetadataOfFile](/_site/assets/ohsint/ohsintmetadata.png)

Another way we can do this if you have a Linux system is to run the command exiftool on the file.

![MetadataOfFileUsingExiftool](/_site/assets/ohsint/ohsintexif.png)

As you can see we get the same information from both methods. The important information here is the copyright - "OWoodflint", the name of the person who owns the image. If we google this we will get some interesting results: a twitter page, a blog, and a Github repository.

![SearchResults](/_site/assets/ohsint/searchresults.png)

Let's take a look at the twitter page first. This will give us the answer to the first question - "What is this user's avatar of?". It's a cat!

![TwitterPage](/_site/assets/ohsint/twitter.png)

We can also get some interesting information here - they have (stupidly) posted their BSSID on their twitter page. We can use this to work out their location! Go to wigle.net (you will need to make an account for this) and perform a Basic Search using the BSSID. A result called UnileverWifi will appear, double-click it and the map will drop you right on the city - they are in London!

![WigleResults](/_site/assets/ohsint/wigle.png)

This search gives us the answer to two questions. The city - London. The SSID - UnileverWifi. <br>
Now we can move on from the Twitter page. Let's look at the Github repository next.

![GithubRepo](/_site/assets/ohsint/github.png)

Straightaway we have our next two answers, the personal email address and we website we found it on!<br>
Now we can move to the blog for the final two questions.

![WordpressBlog](/_site/assets/ohsint/blog.png)

We can immediately see that Oliver has been very open about his holidays, and he is in New York!<br>
Now we only have one task left, to find Oliver's password. Normally to find passwords we would need to do some hacking or password cracking, but this is an OSINT room, so we can rule those methods out. We can take a look around the blog, but we won't find much. Let's take a look at the source code of the main blog page. <br>

There is a lot to look through, but when we scroll down to the main code for the blog page, we can spot something looking a little out of place.

![Pass1](/_site/assets/ohsint/pass1.png)

This is our password! Reading the code, we can see it is in the main body of the blog page, just in white. So if we go back and highlight that area, we can see it sneakily hidden in (almost) plain sight!

![Pass2](/_site/assets/ohsint/pass2.png)

That brings us to the end of this room. Fairly easy once you get the search results but I still had fun with it!





