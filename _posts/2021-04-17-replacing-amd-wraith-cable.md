---
layout: post
title: "DIY: Replacing the AMD Wraith RGB Cable (USB version)"
subtitle: |
  The process for replacing ANY proprietary cable, no matter how specific.
# gh-repo: daattali/beautiful-jekyll
# gh-badge: [star, fork, follow]
tags: [test]
comments: true
# published: false
---

# What you need to follow along

- Some amount of knowledge about computers, and their internals
- About a month to wait for AliExpress shipping

# The predicament

Months ago, my brother's PC died, and he got it "repaired" at a local shop
(I was going to look at it but never got around to it).

^(Not to let my saltiness show, the shop's "repair" was just to replace every part in the case. On arrival, the PC still had intermittent hangs until I updated the BIOS, by which time my brother had given up & bought a gaming laptop.
I guess the upshot was that I got his now spare computer, which I'm using as a server.)

The PC shipped with a Ryzen 7 with an AMD Wraith Prism cooler.

The RGB wasn't being detected by my system.
The AMD Wraith Prism's RGBs have two options for control cables - I opened the case up to figure out which was in use.
Turns out the guys that built it never bothered connecting any, and they never provided the unused parts from the build 😡.

It probably serves me right for being slack & not looking at the computer myself/not building it myself, but, lessons learned I guess.

## Replacement options

When I looked into sourcing a replacement, unsurprisingly, this very specific cable was not easy to find, and not particularly cheap -
In the order of $50 AUD.

Though at first glance, these connectors appear to be very specific, and totally unique to the product, I suspected that ultimately,
it tends to be cheaper, easier, and more convenient for manufacturers to use standard parts in their connectors.

If I can figure out what those are, I can make one of these myself.

# Research

## What you need to know to match a connector to a picture

### The configuration of the pins on both ends of the cable

You need to be able to match the lines on each side of the connection to ensure that
the right pin on the board is connecting to the right pin on the peripheral (The RGB).

Getting this right is _very_ important, since if we make a mistake, the potential consequences
may include:

* Shorting VBus to GND
  * VBus is our +5V power supply, and GND is its complement. 
  * These two work in tandem to power many things in our computer
    * If you put something (/a load) between VBus & GND, the voltage difference drives a current
      through the thing/load.
    * How "difficult" it is to power the load (The load's impedance/resistance) is what determines
      how much current goes through the load.
    * This is Ohm's Law:
      * `current = voltage / resistance`.
  * Cables are designed to be very easy to put current through - They're just there to connect things to each other.
    * In other words, cables have a very low resistance, almost no resistance.
  * If we accidentally connect VBus to GND, we get the following:
    * `current = voltage / resistance`. 
    * as resistance approaches 0:
    * `current = 5V / 0`
    * `current ~= infinity`
  * Infinity current is not something we want in our computer. Some part of your computer will begin to smoke,
    and now whichever part that was is no longer a functioning part.

We need to ensure we understand what line connects to what on each side.

### The form factor of the connector / plug / socket

You also need to be able to match the physical plug itself on either side.

The primary things you need to know if you want to match a connector to a picture are:

* The number of connections
* The dimensions of the housing
* The distance between each pin - AKA the "pitch"

The fundamental outcome of getting this wrong is that you:

* Wind up with a plug that just doesnt fit into a socket,
* Out of pocket a few dollars, &
* Waiting another month for AliExpress to ship you the correct parts

We also DON'T want to get this wrong - it's inconvenient.

## Matching the connector

As explained, matching the pins on the peripheral to the pins on the board is *very* important to get right,
as a mistake could be disasterous.

Matching the connector form factor is less important, as if you mess up, at least you don't break anything (usually).

Fortunately, matching the pins was (in this instance) a fairly easy process.
The form factor took more work.

### Matching the pins

It's time to start searching for AMD Wraith Prism cable pictures- Searching this a while
yielded [this reddit post](https://www.reddit.com/r/AMDHelp/comments/hmfmy7/lost_wraith_prism_cable_need_help/).

The post is a cry for help in replacing one of their control cables - They're missing the 4 pin cable on the right,
but they still have the 3 pin cable on the left.

![picture of AMD Wraith Prism connections](/assets/img/amd_wraith/david_moss91_missing_cable.jpg)

The cable on the left is the one we need to replace. This picture is simple but conveys a lot of information.

In particular, we can see 3 colours on the cable, white, green, and black.

These colours are significant, as they are well documented in the USB2 standard, but to be safe,
let's review another post on the matter.

Reddit user OutrageousOkona asks: [Found in my cable drawer, what’s the smaller connector and what could it connect to a usb header? Thanks!](https://www.reddit.com/r/pcmasterrace/comments/g2dy9w/found_in_my_cable_drawer_whats_the_smaller/)

![OutrageousOkona: Found in my cable drawer, what’s the smaller connector and what could it connect to a usb header? Thanks!](/assets/img/amd_wraith/OutrageousOkona_01.jpg)

He gives us some excellent closeups (Which I will use for form factor), and commenters seem to think it matches,
though oddly enough, OP doesnt own an AMD Wraith Prism:

> > it looks like the connector for the AMD Wraith Prism Stock Cooler.
>
> It does rather, I don’t own one though. Serves me right for not making a note of it ages ago.

Let's take note of the other side, though. We can see a 9 Pin USB2 female header cable.
Take note of the colours on the 9 pin connector- We can see green is *just* visible for the middle socket.

It's hard to say for sure, but it also looks like white *might* be visible for the rightmost connection.

Is there any way to verify this configuration?
Well, fortunately this is very well documented as a convention in the USB2 standard - [frontx.com agrees](https://www.frontx.com/cpx108_2.html)

![Diagram of USB header pinmaps with colour conventions labeled](/assets/img/amd_wraith/frontx_usb_pin_map.jpg)



### Matching the form factor
