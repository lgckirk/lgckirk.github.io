---
title: Node.js Event
date: 2019-04-02 17:17:24
tags:
- Node.js
---

A good article to get started: [Understanding Node.js Event-Driven Architecture](https://medium.freecodecamp.org/understanding-node-js-event-driven-architecture-223292fcbc2d).

# EventEmitter

Event is one of the core concepts in Node.js. Read the [official documentation](https://nodejs.org/api/events.html).

Some notes:

## Listeners are called synchronously in the order they were registered

According to the doc:

"When the EventEmitter object emits an event, all of the functions attached to that specific event are called synchronously."

Note it's __called__ synchronously.

See [reference](https://nodejs.org/api/events.html#events_asynchronous_vs_synchronous).
Also see [emitter.emit](https://nodejs.org/api/events.html#events_emitter_emit_eventname_args).

## "this" of a listener is intentionally set to the EventEmitter

Unless you use ES6 arrow function.

[Reference](https://nodejs.org/api/events.html#events_passing_arguments_and_this_to_listeners)

## The number of listeners of an EventEmitter has a soft limit

It will result in a warning when the limit is reached.
[Reference](https://nodejs.org/api/events.html#events_eventemitter_defaultmaxlisteners).

This is to help find memory leak. You can also [set it to unlimited](https://nodejs.org/api/events.html#events_emitter_setmaxlisteners_n).

## "error" is a special event

Emitting an `error` event is like throwing exception. It will crash the program if not handled.

## One-time listener

[One-time listeners](https://nodejs.org/api/events.html#events_emitter_once_eventname_listener) are removed before firing.

That's the only special thing about them.

i.e. They share the same listener queue with regular listeners.

Underneath the hood, these listeners are wrapped by a wrapper function that implements the special behavior.

This wrapper is used internally. For example, `emitter.listeners` will still return the original callback.
But you can use [emitter.rawListeners](https://nodejs.org/api/events.html#events_emitter_rawlisteners_eventname) to get the wrapper function.

```JavaScript
const emitter = new EventEmitter();
emitter.once('log', () => console.log('log once'));

// Returns a new Array with a function `onceWrapper` which has a property
// `listener` which contains the original listener bound above
const listeners = emitter.rawListeners('log');
const logFnWrapper = listeners[0];

// Logs "log once" to the console and does not unbind the `once` event
logFnWrapper.listener();

// Logs "log once" to the console and removes the listener
logFnWrapper();
```

## "removeListener" removes only 1 listener at a time

If you added a single listener function for a single event multiple times, the most recently added one is removed.
i.e. Not all of them are removed by a single `removeListener` call.

See [emitter.removeListener](https://nodejs.org/api/events.html#events_emitter_removelistener_eventname_listener).
