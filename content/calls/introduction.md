---
pcx_content_type: overview
title: Introduction
weight: 2
---

# Introduction to Cloudflare Calls

Cloudflare Calls can be used to add realtime audio, video and data into your applications. Cloudflare Calls uses WebRTC, which is the lowest latency way to communicate across a broad range of platforms like browsers, mobile and native apps. 

Calls integrates with your backend and frontend application to add realtime functionality.

## Why Cloudflare Calls exists

- **It's difficult to scale WebRTC**: Many struggle scaling WebRTC servers. Operators run into issues about how many users can be in the same "room" or want to build unique solutions that don't fit into the current concepts in high level APIs.

- **High egress costs**: WebRTC is expensive to use as managed solutions charge a high premium on cloud egress and running your own servers incur system administration and scaling overhead. Cloudflare already has 300+ locations with upwards of 1,000 servers in some locations. Cloudflare Calls scales easily on top of this architecture and can offer the lowest WebRTC usage costs.

- **WebRTC is growing**: Developers are realizing that WebRTC is not just for video conferencing. WebRTC is supported on many platforms, it mature and well understood.

## What makes Cloudflare Calls unique

- **Unopinonated*: Cloudflare Calls does not offer a SDK. It instead allows you to access raw WebRTC to solve unique problems that might not fit into existing concepts. The API is deliberately simple.

- **No rooms**: Unlike other WebRTC products, Cloudflare Calls lets you be in charge of each track (audio/video/data) instead of offering abstractions such as rooms. You define the presence protocol on top of simple pub/sub. Each end user can publish and subscribe to audio/video/data tracks as they wish.

- **No lock-in**: You can use Cloudflare Calls to solve scalability issues with your SFU. You can use in combination with peer-to-peer architecture. You can use Cloudflare Calls standalone. To what extent you use Cloudflare Calls is up to you.

## What exactly does Cloudflare Calls do?

- **SFU**: Calls is a special kind of pub/sub server that is good at forwarding media data to clients that subscribe to certain data. Each client connects to Cloudflare Calls via WebRTC and either sends data, receives data or both usign WebRTC. This can be audio/video tracks or DataChannels.

- **It scales**: All Cloudflare servers act as a single server so millions of WebRTC clients can connect to Cloudflare Calls. Each can send data, receive data or both with other clients.

## How most developers get started

1. Get started with the echo example, which you can download from the Cloudflare dashboard when you create a Calls App or from [demos](/calls/demos/). This will show you how to send and receive audio and video.

2. Understand how you can manipulate who can recieve what media by passing around session and track ids. Remember, you control who receives what media. Each media track is represented by a unique ID. It's your responsibility to save and distribute this ID.

{{<Aside type="note" header="Calls is not a presence protocol">}}

Calls does not know what a room is. It only knows media tracks. It's up to you to make a room by saving who is in a room along with track IDs that unique identify media tracks. If each participant publishes their audio/video, and receives audio/video from each other, you've got yourself a video conference!

{{</Aside>}}

3. Create an app where you manage each connection to Cloudflare Calls and the track IDs created by each connection. You can use any tool to save and share tracks. Check out the example apps at [demos](/calls/demos/), such as [Orange Meets](https://github.com/cloudflare/orange), which is a full-fledged video conferencing app that uses [Workers Durable Objects](/durable-objects/) to keep track of track IDs.
