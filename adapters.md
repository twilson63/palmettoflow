# Adapters

Palmetto Flow adapters are plugable write-logs that can be swapped out of any palmetto flow application.  The write-log or stream is the core implementation of the palmetto flow, it manages all the events and routes them to the intended parties.

* [palmetto-fire](https://github.com/twilson63/palmetto-fire)
* [palmetto-couchdb](https://github.com/twilson63/palmetto-couchdb)
* [palmetto-rmq](https://github.com/twilson63/palmetto-rmq)
* [palmetto-redis](https://github.com/akennedy/palmetto-redis)
* [palmetto-pubnub](https://github.com/twilson63/palmetto-pubnub)

These adapters implement the same api so that they can be interchangable:  

## API

The api uses the NodeJS EventEmitter Object:

``` js
var ee = palmetto(config)

ee.on('foo', function (event) { })
ee.once('foo', function (event) { })
ee.emit('send', event)
```

You can and should use the api on both the presentation side and the data side of your application, if you use fire, then you will be using `firebase` as your `log`, if you use the rmq adapter, you will be using RabbitMQ as your `log`.

## Config

The only difference between the adapters is the configuration:

* endpoint
* app

All implementations requires an `endpoint` node, which is the resource identifier to the `log` server.  
All implemenations requires an `app` node, which identifies the `log` events, for firebase it is a key, for couchdb it is a database, for rmq it is a queue.  

For other configuration details please see each individual adapter.

## FAQ

* Can I mix and match adapters, for example use fire for client and couchdb for the data service?  

No, unless you replicate log data between couchdb and firebase.

* How do I handle security?

There are several ways to handle security, but none or unlike the same concerns with a monolith application.  There will be several examples and discussions available.

* Can I implement my own adapter?

Yes, it is pretty easy, if you look at the examples, you simply need to provide a NodeJS event emitter to your presentation or data services layer.

* These are all in NodeJS, can I use other languages for implementaions?

Absolutely, it is basically pub/sub, so you need a way in each language or framework to handle incoming subscriptions and publishing messages.  You may want to look at some of the firebase or pubnub.

* How do I replay my events?

My current recommendation is to use a logging service that captures every message and writes them to a persistence store like s3 and then removes the events from the `log`, then use a `consumer` or s3 reader that reads each event in the order it was created. I still need to experiement, but plan to have a log service for each of the above adapters which will persist each event to s3, then a s3 event loader app that will build up a data store from the s3 bucket.  This should make it pretty easy to rebuild data stores if you should lose a data store, as well as make the `log` lean
