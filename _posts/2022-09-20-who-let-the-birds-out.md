---
title: Who let the birds out?
author: Andreas Wienes
date: 2022-09-20 - 16:25:26 +0100
categories: [HACKING]
tags: 
  - "infosec"
toc: true
---

## Some General Information about Bird E-Scooters

Bird e-scooters are becoming more and more popular in bigger cities. And despite the fact that they are laying around like pieces of ugly looking electronic trash, they are sometimes  actually quite useful. 

![bird_twitter](/assets/img/bird_trash.jpeg)

And they are easy to get. You just need to open the nice looking mobile app, find a bird nearby and then finally book it. That's it. - Enjoy your ride!

Just in case you can't find the desired bird for some reason you are also able to use a nice little feature to let the bird chirp. Making some kind of noice and blinking lights to help you with a little orientation, when it's dark outside. 
 

## Let's have some fun

Analyzing the network traffic between the Bird mobile app and the Bird servers shows two interesting API endpoints that are used to help you getting your next ride.

`https://api-bird.prod.birdapp.com/bird/nearby` and `https://api-bird.prod.birdapp.com/bird/chirp`.

The first one is used to get a list of all birds within a specific radius and the second one is used to let a Bird chirp.

Sounds great, eh?

What what would happen if someone would try let more than one Bird chirp?

Well, there is nothing stopping you from trying to do this.

[Here is a short demonstration](https://www.youtube.com/watch?v=hAcBdksJkbk&ab_channel=HackLikeDemons) (a click will open YouTube)
 

Imagine someone would add different locations, where a lot of Birds are located, into this [proof of concept](https://github.com/HackLikeDemons/let_the_birds_chirp).
Imagine someone would set the radius to a very high number and put all of this into an infite loop... Ooops. 

I'm pretty sure the same is possible with other providers such as Tier, but I didn't have the time to test it.

## Learnings

### Limits everywhere

![bird_twitter](/assets/img/bird_limits_everywhere.png)

The Bird API should have different types of limits implemented. The allowed value for the radius should be limited. The number of Birds you receive from the API is limited to 250. But do you really need information about 250 Bird E-Scooter nearby? This value should also be limited. And the number of requests we are able to send to `/bird/chirp` within a reasonable amount of time should also be limited.

### Make it easy to get in contact

The people at Bird don't use [/.well-known/security.txt](https://securitytxt.org/) so I've tried to contact them via Twitter and e-mail.
This is what I got in response:

![bird_twitter](/assets/img/bird_twitter.png)
![bird_my_email](/assets/img/bird_my_email.png)
![bird_email_answer](/assets/img/bird_email_answer.png)

So please as a company use the security.txt or start a bug bounty program to make reporting security findings easier. 

Thanks for reading and thanks a lot to [https://twitter.com/Zyberum](https://twitter.com/Zyberum) for the inspiration for this little experiment.

