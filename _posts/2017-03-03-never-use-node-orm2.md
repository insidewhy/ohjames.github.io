---
layout: post
title:  Never use node-orm2
date:   2017-03-03 00:15:00
categories: node javascript
---

node-orm2 is terrible. Don't use it.

1. Promises are the best way to handle asynchronous results now, especially with the advent of [async/await](https://blog.risingstack.com/async-await-node-js-7-nightly/). Yet async/await won't help you with node-orm2 because it uses callbacks everywhere. Sure you can use a library like [async](https://github.com/caolan/async) to avoid [callback hell](http://callbackhell.com/) but promises are much better (even when discounting async/await) because they are [composable](https://gist.github.com/domenic/3889970). This is why they are part of every new HTML5 proposal involving asynchronous results (e.g. the [fetch API](https://developer.mozilla.org/en/docs/Web/API/Fetch_API)). However node-orm does decide to [provide its own class called Promise](https://github.com/dresende/node-orm2/blob/v3.2.3/lib/Promise.js) to override node's superior built-in implementation with, one that isn't at all compatible, or very useful.
2. The library does [classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) all wrong. Instead of using ES6 classes or `prototype` it assigns a new copy of each method in the [constructor](https://github.com/dresende/node-orm2/blob/v3.2.3/lib/Model.js#L205) [one](https://github.com/dresende/node-orm2/blob/v3.2.3/lib/Model.js#L223) by [one](https://github.com/dresende/node-orm2/blob/v3.2.3/lib/Model.js#L251). This is bad for memory usage and bad for performance.
3. It's [slow](https://github.com/rafaelkaufmann/q-orm/issues/1#issuecomment-64449143) and the API is [non-uniform](https://github.com/rafaelkaufmann/q-orm/issues/1#issuecomment-64442225). People who've had to use it in production don't have very [good](https://www.reddit.com/r/node/comments/3bye2l/has_anyone_used_an_orm_with_nodejs_that_they/cst8k5k/) [things](https://github.com/rafaelkaufmann/q-orm/issues/1#issuecomment-64449791) to say about it.
4. The documentation is incomplete, some things are only documented on [github](https://github.com/dresende/node-orm2/blob/v3.2.3/Readme.md) and others are only documented on the [wiki](https://github.com/dresende/node-orm2/wiki).
5. It is not an active project, there were only [24 commits last year](https://github.com/dresende/node-orm2/commits/master) and some PR have [been open for over 2 years without response](https://github.com/dresende/node-orm2/pull/574).
6. It [bundles all supported database drivers](https://github.com/dresende/node-orm2/tree/v3.2.3/lib/Drivers/DML) and other utilities you may or may not need like a [middleware for express](https://github.com/dresende/node-orm2/blob/v3.2.3/lib/Express.js).
7. Many annoying niggles, e.g. after disconnecting from the database you can't reconnect without restarting node.

You might want to [question if you really need ORM at all](http://www.bigdatalittlegeek.com/blog/2014/3/18/orm-the-killer-of-scalability) or use a library with better standards support, better code and better documentation such as [sequelize](http://docs.sequelizejs.com/en/v3/) or [mongoose](https://github.com/Automattic/mongoose).
