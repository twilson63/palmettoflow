<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Services

The service is responsible for business logic and data persistence, each service controls their own data store.  When registering a service it is important that the service can only listen to data events and submit/emit events from the write log.  This is how it communicates with the outside world.

``` js

module.exports = service;

function service(ee) {

  ee.on('model-verb', function(object) {
    // handle event request
    emit('response', object);      
  });

  ee.on('widget-create', function(e, write) {
    // if authorized then create the widget
    ee.on('auth-response', function(a) {
      if (a.ok) {
        // insert e.object into db
        write({
          id: 1,
          ok: true
        });
      }
    });
    // ask session service if user is authorized to create a widget
    ee.emit('response', {
      verb: 'auth',
      model: 'session',
      actor: e.actor,
      object: {
        name: '' 
      }
    });
    
  })
}


```

It is important the service container consumes messages from the write log based on the event type and verb.  Then inside the application service container it emits the events messages that match the type and verbs specified in the registered method.

The above example is letting the app service container subscribe to the `write log` and filter all of the basic information from an event message:

* verb
* type
* transaction
* system

and just pass to the service the object and the actor.  Then the service can listen based on the verb using the `on` method.  It can do its work and then push back the results using the `write` method.  The application service container would marry the response with the sent in verb, type, transaction, system.

The main goal is to have a service like `widgets` to be re-usable in many different applications without having to have know specific details of that application other than its piece.



