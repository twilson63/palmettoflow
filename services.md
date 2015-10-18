<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Services

The service is responsible for business logic and data persistence, each service controls their own data store.  When registering a service it is important that the service can only listen to data events and submit/emit events from the write log.  This is how it communicates with the outside world.

``` js

module.exports = service;

function service (config) {
  // manage any config info
  return function (ee) {
    ee.on('/model/verb', function(object) {
      // do stuff
      // return response
      emit('send', responseEvent);      
    });
  }
}

```

The above example is a service that takes in a configuration object and returns a function that is looking for a palmettoflow adapter, the adapter will emit palmettoflow events using the following json schema

``` js
{
  "title": "palmettoFlow-event",
  "type": "object",
  "properties": {
    "to": {
      "type": "string",
      "description": "for calls to service use /:domain/:category/:service/:action"
    },
    "from": {
      "type": "string",
      "description": "a unique identifier that can be used to return response"
    },
    "object": {
      "type": "object",
      "description": "the data that is needed to process the event"
    },
    "subject": {
      "type": "string",
      "description": "the name of the event"
    },
    "verb": {
      "type": "string",
      "description": "the action that event is trying to perform"
    },
    "actor": {
      "type": "object",
      "description": "the initiator of the event"
    },
    "dateSubmitted": {
      "type": "string",
      "description": "the date the event was initiated"
    },
    "duration": {
      "type": "string",
      "description": "the time in milliseconds the event took to process"
    }
  },
  "required": ["to","from","object"]
}
```


and just pass to the service the object and the actor.  Then the service can listen based on the verb using the `on` method.  It can do its work and then push back the results using the `ee.emit('send', {})` method.  The application service container would marry the response with the sent in verb, type, transaction, system.

The main goal is to have a service like `widgets` to be re-usable in many different applications without having to have know specific details of that application other than its piece.


## Open Source Services

* [Simple Queue Service](https://github.com/twilson63/palmettoflow-queue-svc)
* [PouchDB/CouchDB Service](https://github.com/twilson63/palmettoflow-pouchdb-svc)
* [MySQL Service](https://github.com/twilson63/palmettoflow-mysql-svc)
* [Auth0 Service](https://github.com/twilson63/palmettoflow-auth0-svc)



