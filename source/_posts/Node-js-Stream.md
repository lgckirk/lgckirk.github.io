---
title: Node.js Stream
date: 2019-04-02 22:58:29
tags:
- Node.js
---

Here is a good article about the stream interface in Node.js: [Node.js Streams: Everything you need to know](https://medium.freecodecamp.org/node-js-streams-everything-you-need-to-know-c9141306be93).

Here is the official documentation for the [Stream module](https://nodejs.org/api/stream.html).

There are also functions in other modules that creates/operates on streams.
For example, the [Readline module](https://nodejs.org/api/readline.html) reads lines from a readable stream.

# Stream

Stream is a collection of data with well defined input/output that takes/serves chunks of data.

## Types of stream

There are 4 types of streams in Node.js
* [Readable stream](https://nodejs.org/api/stream.html#stream_readable_streams)
* [Writable stream](https://nodejs.org/api/stream.html#stream_writable_streams)
* [Duplex stream](https://nodejs.org/api/stream.html#stream_class_stream_duplex)
* [Transform stream](https://nodejs.org/api/stream.html#stream_class_stream_transform)

Transform stream is very similar to duplex stream. The difference, in brief, is that for duplex stream, the readable and writable (sub)streams are separate whereas for the transform stream, they are kind of one. Here is a good [stackoverflow answer](https://stackoverflow.com/questions/18335499/nodejs-whats-the-difference-between-a-duplex-stream-and-a-transform-stream) explaining the difference.

## Consume streams

The easiest way to consume stream is through the `readableStream.pipe(writableStream)` function.

If you need more flexibility for custom things, use events. 

For more, refer to the article.