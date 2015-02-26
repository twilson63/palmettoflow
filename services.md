<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Services

The service is responsible for business logic and data persistence, each service controls their own data store.  When registering a service it is important that the service can only listen to data events and submit/emit events from the write log.  This is how it communicates with the outside world.

``` js

myservice.register = register;
module.exports = myservice;

function myservice(env, ee) {

  ee.on('query', function(e, write) {
    // handle event request
    write([{ foo: 'bar' }]);      
  });

  ee.on('create', function(e, write) {
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
    ee.emit({
      verb: 'auth',
      type: 'session',
      actor: e.actor,
      object: {
        verb: 'create',
        type: 'widget'
      }
    });
    
  })
}

function register() {
  return {
    type: 'widget',
    verbs: ['query', 'create']
  }
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



