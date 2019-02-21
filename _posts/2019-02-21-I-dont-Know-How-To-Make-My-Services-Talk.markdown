---
layout: post
comments: false
title:  "I dont know how to make services talk"
excerpt: "Lets explore the service communication options."
date:   2019-02-21 11:00:00
mathjax: false
---

This post is more of an assimilation of various options that are out there ,to make my service A talk to service B. This is a bit of an intersting space where an architect is always in the delimma of choosing rhe right approach . 
Lets try to get our hands a bit dirty, and may the force be with us...

To start with we have a traditional monolithic application . My architect was able to do one of the most difficult tasks,i.e. break this monolith into logical components ,so that each of these ,can be designed into microservices. These microservices will be true to there name aka, have there own Databases, independently deployed and scaled.
