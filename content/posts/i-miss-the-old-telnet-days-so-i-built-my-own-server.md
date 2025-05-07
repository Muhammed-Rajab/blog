---
date: '2025-05-07T08:23:23+05:30'
draft: false
title: "I Miss The Good Ol' Telnet Days - So I Built My Own Server"
tags: ["c++", "project", "dev-log"]
---

Here's the [_**repo**_](https://github.com/Muhammed-Rajab/telnet.cpp), if you are in a hurry.

OK, I want to set the record straight: Before starting this project, I barely had any idea about telnet and its applications. Come on, what did you expect? I'm 19. **"Old days" - pfff!**

I always saw this word pop-up in networking articles I read, and you'll always find this term in every article that's titled

_**10 Cool Linux Terminal Tricks That You Should Know - And More!**_

So I decided to search it up in my favorite search engine (i use google, btw), and oh boy, was it cool.

## So what's Telnet really all about?

Here's how Wikipedia describes Telnet:

> The telnet protocol is a client-server protocol that runs on a reliable connection-oriented transport. Most often, a telnet client connects over TCP to port 23 or 2323, where a Telnet server application is listening. The Telnet protocol abstracts any terminal as a Network Virtual Terminal (NVT). The client must simulate a NVT using the NVT codes when messaging the server.

Let's go through it like the good programmers we pretend to be are:

**No.**

To me, it's basically a way to connect to a TCP server, get the data, display, and maybe send some data back to the server. That's it. When I hear "Telnet", I'm not thinking about NVT and all that, I'm too young for that.

Personally, telnet is just a cool way for me to watch star wars.

```bash
$ telnet towel.blinkenlights.nl
```

This was all I had in my mind when I read about telnet. A super high budget movie but in terminal rendered in ASCII, moving at a super smooth frame rate and ridiculously high resolution? What more can I ask for?

And when I finally tried it out, here's what I got

```bash
➜ telnet towel.blinkenlights.nl
Trying 213.136.8.188...
```

Well, that sucks.

My dreams were shattered into smithereens. My eyes welled up, hips trembling, spirit crushed. AAHHHHHHHHHHH (dramatic cat noises)

It doesn't matter. We all are meant to be disappointed. Life ain't that easy, girl. Get over it.

This was enough to give me the motivation needed to work on my own TCP server application and I knew exactly what to do.

## Introducing telnet.cpp

A simple TCP server which allows you to go through a grand collection of 2 (as of today) telnet applications. So cool, isn't it? Being as creative as a half-cut potato molding on the bottom shelf of the Fridge, I decided to name it `telnet.cpp`. And yes, I'll be using `C++` for the project, and here are the 13 reasons why I chose to use it:

1. **I hate myself**
2. **I love to boast**
3. **I'll have to use C++ a lot in the near future**
4. **The 'M' is Masochist stands for me**
5. **-**
6. **-**
7. **-**
8. **-**
9. **-**
10. **-**
11. **-**
12. **-**
13. **-**

Sorry, I don't feel obliged to give all the 13 reasons. If you've ever done anything in `C++`, you can probably fill out the rest yourself.

The plan is simple:

- Give the user a menu to choose from.
- On choosing a program, render it to screen, accept user input, etc.
- Make it clean enough and allow multiple users.

This won't be a step-by-step guide on how to make one. The code I wrote is soo clean and self explanatory, even if you never did anything in `C++`, you'll understand pretty much the whole thing, given that you have some idea about sockets in Linux. Yes, we'll be using Linux sockets, not `winsock` (i !use arch, btw).

## Main Menu

It's not much, but it's interactive, eyy. There's a timeout of 30s and the user can select any from the two of the applications (as of now).

![Main Menu](/blog/images/main-menu.gif)

## Telnet App #1: kitty.says()

A wise eye-blinking kitty giving you advice over the wire - could you be any more blessed? The app is quite simple. You store the kitty as frames, pair them with a bunch of quotes, and give the user the ability to go back to the menu, quit or even change the quote. Simple enough, right? It is.

Most of the difficulty you'll be facing here will be related to handling user input. You will struggle a bit with **"IaCs"** (Interpret as Commands), Typeahead buffers, and some other quirky little stuff.

And in the end, I was left with this little thingy:

![kitty.says()](/blog/images/kitty-says.gif)

## Telnet App #2: cube.render()

This... this is it. This was something that I wanted to try for quite some time. A rotating wireframe cube with controls. A few months back I built [terrible-renderer.cpp](https://github.com/Muhammed-Rajab/terrible-renderer.cpp), and it was one of my favorite projects till date. I finally got the chance to understand 3D rendering, and I built something that's very close to my heart - **a fricking spinning DONUT🍩!**

Ever since I started programming, I was so captivated by [Andy Sloane's Donut.c](https://www.a1k0n.net/2011/07/20/donut-math.html). It was my dream to build it myself one day. That _myself_ part is quite important here. I want the math behind the rendering to slowly consume me from my inside, I didn't want to just copy paste the code. And once I got there, I faced another challenge: How can I make this a cube?

There are several videos that explains the math behind the rendering, but it's pretty much the same.
```
Generate Surface Coordinates -> Transformation -> Projection -> Lighting -> Rendering
```

I attempted rendering the surface of the cube and I got a pretty satisfying result. But then I wanted to try something else. Something easier, but fun to do. So I chose to stick with Wireframe (no messy Z-Buffers, haha).

And in the end, I was left with this big thingy,


![cube.render()](/blog/images/cube-render.gif)

As you can see, there are a few controls that you can mess around with to modify the cube's behaviour. Just make sure to press **RETURN** after any control input (That's how the server gets your input).

## In the end...

it doesn't even matter.

Nah, it does. I learned quite a bit from this project. I got to do some Linear Algebra, brush up on `C++`, and brag about the whole thing on Instagram. Ahhhhhh, INNER PEACE 🕊️

The project isn't complete yet. I have to rewrite the server to handle multiple clients. Maybe polish the menu a bit? But I'll be sure to keep you updated here, love 💖.

**UPDATE #1**: Now the server can handle multiple clients, using `std::thread`, and that's awesome✨.
