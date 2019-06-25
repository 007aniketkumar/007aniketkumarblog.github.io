---
layout: post
comments: false
title:  "Million connections.."
excerpt: ""
date:   2019-06-13 11:00:00
published: true
mathjax: false

---

People usually say there are a million connections that are supported by an application XYZ (say twitter, whatsapp). 
What does it really mean? A machine has 65k odd ports , so with 65k ports how does  one open million+ connections . 

Let's try to dimistify all of this .

To start with let's begin with what is really meant by IP , socket , port and how do the packets travel. 
Let us  say , I stay in MG road, in house number 123. This apartment has 1 door. Now if there is a guest who wants to meet me, he will 
first come to the MG road (IP) , then to the house number 123(PORT), eventually enter through the either of the doors (SOCKET).
The MG road can obviously be translated by DNS to a unique longitude , latitude location. For understanding in network terms , let's say
DNS  translates MG ROAD to 10.0.0.0.

MG road(IP) - 10.0.0.0
House number(PORT) - 123
Door(SOCKET) - 10.0.0.0:123

Taking this a bit further , I have 65,535 houses on MG road(I must be a wealthy man!) , still how can I entertain a million guests at a given time.

Drawing pararrel from above analogy, do I really end up buying houses, when I have got many guests coming to my place. Not exactly!
Let's try to solve the below domestic problem , and see if we can answer the above question.

I am having veg and non-veg guests coming at my place, and they are pretty fickle minded, and dont see an eye to eye to each other.What I can really do is, I can have veg cooking process in house 1(port1) and non-veg cooking process in house 2(port 2).
So, now I have tied up the process to my ports.

I have segragated my guests and routed them to correct houses(ports ), but I have still not answered the question for entertaining large number of veg and non veg guests (remember - they are still going to their respective houses /ports) , and there is only one house for each. 
 I will use the same analogy again, my house can have mulitple doors (sockets),I only need to allocate the right door for my guests , so that I can entertain them better, and they do not get blocked, because some one is taking a lot of time get through one door! 
 How do I do that :
 I will say that my Door 1 , is only for my guest, who is coming from Sarjapur and house number 567.
 
 So , now my socket has 5 attributes now :
 
 Door(Socket) - My street address(local IP) + House Number(local port) + Guest Street address(remote IP) + Guest house number(Remote port) .
 
 In case you are wondering , what's the 5th attribute, its the protocol. I have been referring to IP here, but there also be other ways like Http,UDP, depending on what layer of OSI model are we operating at.
 
 A good point to note in the above is, since the socket has both mine as well guest identifier, this is regarded as birectional and is often used for applications like chat services, or where push notifications need to be sent(like sending you the driver details when your cab has arrived)
 
I can have many guests(connections) coming to same house(port) itself, as long as I am able to open as many unique doors for them(sockets) . 
It all boils down to , my entertaining capability(processing capability) at the end, as to how soon can I manage them!


 
 




