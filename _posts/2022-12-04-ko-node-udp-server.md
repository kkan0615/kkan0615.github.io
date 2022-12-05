---
title: How to create UDP server with Node.js.
author: Youngjin Kwak
date: 2022-12-04 18:21:00 +0800
categories: [nodejs]
tags: [nodejs]
image:
  path: ../images/nodejs-logo.jpeg
  width: 800
  height: 500
  alt: nodejs-logo.
---
---
# Overview
This article is going to talk about how to use UDP server in Node.js.

# Set up project
```shell
npm init -y
```
start Node.js package
```shell
npm i ts-node
```
ts-node is used for running typescript file without compiling

# Setup server
```typescript
import { createSocket } from 'dgram'

const server = createSocket('udp4')
server.bind(12778)

server.on('listening', () => {
  const addressInfo = server.address()
  console.log(`Server is working on ${addressInfo.address}:${addressInfo.port}`)
})

server.on('message', (msg, remote) => {
  console.log(`Serve get message: ${msg.toString()} from ${remote.address}:${remote.port}`)
})
server.on('close', () => {
  console.log('Close successfully')
})

server.on('error', (err) => {
  console.log(`server error: ${err.stack}`)
  server.close()
})
```
Server will run on port 12778

## createSocket([type or options] [, callback])
```typescript
import { createSocket } from 'dgram'

const server = createSocket('udp4')
```
createSocket function returns socket object.
### Parameter
types [string]: ```udp4``` or ```udp6``` <br>
or <br>
options
- type [string]: The family of socket. Must be either 'udp4' or 'udp6'. Required.
- reuseAddr [boolean]: When true socket.bind() will reuse the address, even if another process has already bound a socket on it. Default: false.
- ipv6Only [boolean]: Setting ipv6Only to true will disable dual-stack support, i.e., binding to address :: won't make 0.0.0.0 be bound. Default: false.
- recvBufferSize [number]: Sets the SO_RCVBUF socket value.
- sendBufferSize [number]: Sets the SO_SNDBUF socket value.
- lookup [Function]: Custom lookup function. Default: dns.lookup().
- signal [AbortSignal]: An AbortSignal that may be used to close a socket.

and <br>
callback [Function] : Attached as listener to ```message``` events

## bind([port][, address][, callback]) function
```typescript
server.bind(12778)
```
bind function is used for binding port and address. <br>
If address is not passed, default is 0:0:0:0.

## on()
Listen events.

| Events       | Description                                                               |
|--------------|---------------------------------------------------------------------------|
| close        | It's emitted after a socket is closed with ```close()``` functions        |
| connect      | It's emitted after a socket is connected with remote address successfully |
| error        | It's emitted after a socket encounters errors                             |
| listening    | It's emitted once after ```bind``` functions                              |
| message      | It's emitted whenever a new message buffer is available on socket         |

## close([callback])
Close socket and stop listening for buffer data

# Setup client
```typescript
import { createSocket } from 'dgram'

const client = createSocket('udp4')
client.bind(12777)

let clientCount = 0
const interval = setInterval(() => {
  const messageBuffer = Buffer.from(`Client send a data to server. Time: ${new Date().toISOString()}`)
  client.send(messageBuffer, 0, messageBuffer.length, 12778, (error, bytes) => {
    if (error) {
      console.error(error)
      throw error
    }
    if (clientCount++ >= 10) {
      client.close()
      clearInterval(interval)
    }
  })
}, 1000)
```
- client will run on port 12777
- Client will send a message buffer to sever every 1 second

### socket.send(msg[, offset, length][, port][, address][, callback])
```typescript
const messageBuffer = Buffer.from(`Client send a data to server. Time: ${new Date().toISOString()}`)
client.send(messageBuffer, 0, messageBuffer.length, 12778, (error, bytes) => {
  if (error) {
    console.error(error)
    throw error
  }
  if (clientCount++ >= 10) {
    client.close()
    clearInterval(interval)
  }
})
```
Send message buffer to port and address which are passed as parameters.

### Multiple
```typescript
const data1 = Buffer.from('hello');
const data2 = Buffer.from('world');

client.send([data1, data2], 12778, (error) => {
  if (error) {
    console.error(error)
    throw error
  }
})
```
```send()``` function allows to send more than one message buffer to the server.
server will receive data as a combined message like```helloworld```

# Ref
[Node.js document](https://nodejs.org/api/dgram.html)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)