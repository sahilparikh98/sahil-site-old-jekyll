---
layout: post
title: UDP vs TCP for live video streaming
subtitle: It's not as hard to pick as you think
tags: [test]
comments: true
---

Typically live video-streaming appliances are not designed with TCP streaming in mind. If you use TCP, the OS must buffer the unacknowledged segments for every client. This is undesirable, particularly in the case of live events; presumably your list of simultaneous clients is long due to the singularity of the event. Pre-recorded video-casts typically don't have as much of a problem with this because viewers stagger their replay activity; therefore TCP is more appropriate for replaying a video-on-demand.

IP multicast significantly reduces video bandwidth requirements for large audiences; TCP prevents the use of IP multicast, but UDP is well-suited for IP multicast.

Live video is normally a constant-bandwidth stream recorded off a camera; pre-recorded video streams come off a disk. The loss-backoff dynamics of TCP make it harder to serve live video when the source streams are at a constant bandwidth (as would happen for a live-event). If you buffer to disk off a camera, be sure you have enough buffer for unpredictable network events and variable TCP send/backoff rates. UDP gives you much more control for this application since UDP doesn't care about network transport layer drops.

I learned pretty much most of this from my computer networks course taught by Dr. Stephany Coffman-Wolph, here at UT.
