---
date: 2019-12-26 23:00:00
layout: post
title: Angulars async pipe may be a pest
subtitle: Useful but a performance-killer
description: >-
  The async pipe is useful to semi sync access observable-data in an angular template. 
  But even in smaller datasets its still a waste of resources when there's a huge amount of dependencies changing.
image: https://angular.io/assets/images/logos/angular/angular.png
optimized_image: https://angular.io/assets/images/logos/angular/logo-nav@2x.png
category: angular
tags:
  - angular
  - performance
author: nilslappe
---

The Async-Pipe provided by angular is quite a handy tool to keep your code tidy.
Just put the `observable$ | async` in your template and you get your data without any subscription boilerplate.

right? But should you really use it?
I'd say... it depends.
Small applications with just a few nested components, few services etc. wont suffer a big performance hit.
But, if your application grows bigger you should really consider to use more boilerplate subscriptions. 

Why do i mention this? Well, the team i work in currently develops quite a huge platform. 
We initially used tons of Async-Pipes just because it saved a bunch of already mentioned boilerplate subscriptions.
A ton of services, routes, components and pages later we faced a big Problem. The platform turned unbearable slow. 
Every click, every navigation, every interaction that triggered a change-detection (CD) let the CPU load rise to 100% for a bunch of seconds and more or less froze the view.
It took quite a bit of testing and debugging to find the issue, but in the end we could heavily improve the responsiveness of pretty much everything by getting rid of all the Async-Pipes.

The actual Problem is not really the Async-Pipe itself, but the combination with the CD.
If there are lots of dependencies, services and components updating values everywhere, the CD triggers all the inputs, directives, pipes etc. in the template to update aswell.
Therefore the Async-Pipe will wait and unfold the observable countless times. This requires computing time and will eventually slow your App down.
Getting the observable, unfolding it, checking if the observable changed, passing it on and also interpreting the template-micro-language pipe call will require more CPU time than passing a fixed value that was updated by a subscription just once after the source changed.
Especially if the CD updates the inputs about 25-times... each of them...

So, if you develop a bigger app and it feels kinda slow, try to exchange all your Async-Pipes with regular Subscription boilerplate - it will probably help.

I cant share Code samples of the real deal, as it is property of the company i work for. But i prepared a small github repo to enable you to try and test it out.
As the repo is really basic, the problem basically doesnt exist there - but you can take a look at both implementations and try it out in your app.
You found this post, so you are probably looking for something i described, right? ;)

You can look at the repo here: https://github.com/nlappe/dev-life_2019-09-13-angulars-async-pipe-a-pest
