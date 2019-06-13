---
layout: post
comments: false
title:  "I dont know how to make services talk-Post 2"
excerpt: "Service Mesh, Gateway can I use them."
date:   2019-03-20 11:00:00
mathjax: false
---

This is the continuation of the first series of blog <a href =" https://007aniketkumar.github.io/2019/02/21/I-dont-Know-How-To-Make-My-Services-Talk/">post</a>, where we talked about the options of using an orchestration based pattern against a choreographer. 


The answered question was where should my routing logic reside. How about the security features, entitlements, logging, tracing. Who should be responsible for handling this? Should I use an API gateway? How about service Mesh. But wait what do these jargons actually mean.

Let us try to demystify them:

One of the basic definitions that come to mind is, an API gateway handles the North-South traffic, whereas service Mesh handles the East-west traffic. North-South traffic essentially means the requests that are coming at the edge of a cluster from an external client. This is also known as ingress(incoming) and egress(outgoing) especially in the kubernetes world.

A popular analogy can be, when you type www.amazon.in, the request then hits the API gateway of Amazon, which then routes the request to either the desktop site or mobile site.
Of course, a lot of other complications(DNS, CDN ) play some role as well, but let's just tell them Not TODAY!.

Now my services can run on ephemeral nodes and register themselves on zookeeper /Eureka which in turn talks to the API gateway. 
An example of the above implementation can be found under these projects

Basic student <a href = "https://github.com/007aniketkumar/EurekaStudentService">service</a>
The docker image can be downloaded using : docker pull 007aniketkumar/student_eureka_service

Eureka <a href = "https://github.com/007aniketkumar/EurekaStudentServer">server</a> (where the services register themselves, Zookeeper is another implementation).

Spring Cloud <a href=" https://github.com/007aniketkumar/SpringCloudGatewayEurekaIntegration">Gateway</a>

All my requests are received at the gateway, and it can make intelligent routing decisions(versioning being one), take care of authentication(OAUTH2), perform telemetry, load balance, circuit breaker(Hystrix) among other functions. My client is unaware of the fact, whether it is hitting the gateway or the actual service. 

Popular gateway out there is Zuul(Netflix), Consul(by Hashicorp), APIGEE (Google), Spring Cloud Gateway, etc.
Ngnix is also used in certain places, the basic version out there acts more like a reverse proxy without the additional benefits that are provided above.

Now that we have solved the problem at the edge of the network, how about service to service communication, popularly known as east-west communication. This is where my Service Mesh really shines.

The service mesh can take care of most of the problems that we discussed at the end of the previous post. My application developer needs to worry only about the business logic and the API. 
The service mesh can be as trivial as running a small piece of code on each container, along with my service. The job of this small piece of code is to take care of security, logging, telemetry and also do the all-important job of calling the other service! Of course, it will need to regularly look at some global registry file to figure out the routing details, but now my service is detached of the redundant logic. This kind of pattern is also known as the sidecar pattern. 
Istio has been gaining a lot of popularity in the service mesh design. It employs Envoy as the proxy to run as sidecar with every service. Envoy asks Pilot on the routing details, Citadel on security.

Needless to say, these are interesting times, with the promise of more good things in the pipeline.










