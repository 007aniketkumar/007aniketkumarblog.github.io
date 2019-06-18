---
layout: post
comments: false
title:  "Million Connections-What does it actually mean"
excerpt: "Layman's definitions for understanding this."
date:   2018-12-30 11:00:00
mathjax: false
published: false
---10.0

To start with people usually say there are a million connections that are supported by an application XYZ (say twitter, whatsapp). 
What does it really mean? A machine has 65k odd socktes , so with 65k how does can one open million+ connections . 

Let's try to dimistify all of this .

To start with let's begin with what is really meant by IP , socket , port and how do the packets travel. 
Let us  say , I stay in MG road, in house number 123. This apartment has 1 door. Now if there is a guest who wants to meet me, will 
first come to the MG road (IP) , then to the house number 123(PORT), eventually enter through the either of the doors (SOCKET).
The MG road can obviously be translated by DNS to a unique longitude , latitude location. For understanding in network terms , let's say
DNS gets translated to 10.0.0.0.

MG road(IP) - 10.0.0.0
House number(PORT) - 123
Door(SOCKET) - 10.0.0.0:123

Taking this a bit further , I have 65,535 houses on MG road(I must be a wealthy man!) , still how can I entertain a million guests at a given time.

