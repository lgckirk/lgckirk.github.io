---
title: Node.js Child Process
date: 2019-04-04 00:28:55
tags:
- Node.js
---

Here is a good article about Node.js child process: [Node.js Child Processes: Everything you need to know](https://medium.freecodecamp.org/node-js-child-processes-everything-you-need-to-know-e69498fe970a).

See the official documentation for the [Child Processes module](https://nodejs.org/api/child_process.html).

For reference, [this](https://nodejs.org/api/process.html) is the official doc for the Process module, which represents the main (or parent in this context) process.
Note `process` is a global object so you don't have to explicitly do `require('process')`.

This article, however, is about child process.

# Child Process

Some notes:

## Event 'close' != Event 'exit'

The [close](https://nodejs.org/api/child_process.html#child_process_event_close) event is not the same as the [exit](https://nodejs.org/api/child_process.html#child_process_event_exit) event.

In short, 'close' is triggered when the stdio streams of a child process have been closed.
It is distinct from the 'exit' event, since multiple processes might share the same stdio streams.

The 'exit' event simply means the child process has ended, which doesn't mean its stdio streams are also closed.

## Four child process creation methods

The 4 functions are:
* [spawn()](https://nodejs.org/api/child_process.html#child_process_child_process_spawn_command_args_options)
* [fork()](https://nodejs.org/api/child_process.html#child_process_child_process_fork_modulepath_args_options)
* [exec()](https://nodejs.org/api/child_process.html#child_process_child_process_exec_command_options_callback)
* [execFile()](https://nodejs.org/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)