---
layout: post
comments: false
title:  "I dont know how to make services talk"
excerpt: "Lets explore the service communication options."
date:   2019-02-21 11:00:00
mathjax: false
---

This post is more of an assimilation of various options that are out there ,to make my service A talk to service B. This is a bit of an intersting space where an architect is always in the dilemma of choosing rhe right approach . 
Lets try to get our hands a bit dirty, and may the force be with us...

To start with we have a traditional monolithic application . My architect was able to do one of the most difficult tasks,i.e. break this monolith into logical components ,so that each of these ,can be designed into microservices. These microservices will be true to their name aka, have its own Databases, independently deployed and scaled.

The architect should also try to ensure couple of points:
point 1: Maintain the original sequencing of how the components in my old monolith design were called i.e. component B calls component C and so on. Now that these are microservices, the same sequencing should be maintained.
point 2: He should also look to optimize the design , can my two independent services be called in parallel? This would not helped much when I was dealing with a monolith,as my entire system would have to be scaled on physical machines/VMs/ any other infrastructure.
Keeping the above points in mind, the design could have been as simple as using an orchestrator , which is a kind of controller. The orchestrator could be just another service ,which keeps tab of the order in which the services call each other. Each of my service is just an indepedent component unware of existence of any other service and talks only to the orchestrator service. The orchestrator service is responsible for calling the service and accepting the response from the service. This just makes the orchestrator single point of failure. The failure of orchestrator could just bring my entire syste down . There could be an argument that there can be multiple replicas of my orchestrator to maintain resilience,but there is no denying to the fact that orchestrator still holds the key.

The other option out there is to use a choreography based approach , where my each of my service can listen/subscribe to an event and based on the event received can take the appropriate routing decision. This events can be published on Kakfa cluster(replicated for resiliency) and my services can talk to each other. 

There are still some points to ponder upon , like state management for example - say my service A is dependent on service B which in turn is dependent on service C.In terms of monolith , this would have been one single transaction. 
But now that we have broken our monolith into independent components, how do I handle the above scenario of transaction management.
Is having state absolutely evil in case of microservices...Not eactly (ref - http://highscalability.com/blog/2015/10/12/making-the-case-for-building-scalable-stateful-services-in-t.html)

Moreover, there are cases which justify maintaining stateful services, how you handle the state amongst the services is more important question to answer.(https://microservices.io/patterns/data/saga.html)

In case I use Orchestrator based approach, the transaction management becomes a bit easier , as Orchestrator can take care of undoing all the Database updates, and my services need not take care of this. The biggest drawback is ,I am putting the onus of my application on one single component.

In case of choreography, I can make my services listen to failover/rollback events as well and make them rollback their most recent changes(DB updates/ any other state information).

Both the above approaches, have their own pros and cons and come with their set of baggages, and its upto the architect to choose one over the other.

But wait, using either of the approach , I will end up building a lot of non-application related code within my service. And of course, I have increased the complexity and probably defeated the purpose of building a microservice from my monolith. At the end of isn't my microservice supposed to make things quicker, easier , debuggable! What options do I have now,...lets read the next blog of this series
