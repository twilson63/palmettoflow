<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Stream (write/log)

The stream component is the glue between the components and services.  It is a append-only system that captures activities or events.  It enables software to subscribe to its services in a secure controlled way.  The stream should manage some sort of sequence id, or commit id so that activities or events can be replayed to manage migrations or rebuild persistent stores.

An Activity or Event is the json object that the stream accepts:

As the implementer you can define your own activity/event object, but I recommend that it be consistent and enable to be abstracted so that you can take advantage of several different components and services for you application.

Here is my current design:  (FYI: It still is a work in progress)

``` json

{
  "title": "Event Schema",
  "type": "object",
  "properties": {
    "verb": {
      "description": "Event Action, ie query, create, update, remove, get",
      "type": "string"
    },
    "model": {
      "description": "Data Model that your event is to modify",
      "type": "string"
    },
    "object": {
      "description": "The data of the payload",
      "type": "string"
    }, 
    "actor": {
      "description": "The user/thing who is responsible for the event",
      "type": "object"
    },
    "transaction": {
      "description": "the unique id of the transaction, a transaction may be several events",
      "type": "string"
    },
    "system": {
      "description": "the system id the initial event in a transaction originated from",
      "type": "string"
    },
    "published": {
      "description": "the date the event was publised",
      "type": "string"
    }
  },
  "required": ["verb", "type", "object"]
}
```

So all events that are written to the stream follow this format whether they are generated rom the components or the services, the use this event schema to pass data back and forth.  

Another thing that I have started doing is having consistent names for the verbs in the event object.

* get, get-response
* query, query-response
* create, create-response
* update, update-response

This consistent verb approach should make it very easy to share components and services accross implementation that follow this lead, but not necessary if you implement an application and container service that pushes this naming convention to an implementation detail.

