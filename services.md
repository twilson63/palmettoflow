<img src="palmetto.png" alt="palmetto" align="right" height="100px" width="100px" />

# Services

The service is responsible for business logic and data persistence, each service controls their own data store.  When registering a service it is important that the service can only listen to data events and submit/emit events from the write log.  This is how it communicates with the outside world.

``` js

myservice.register = register;
module.exports = myservice;

function myservice(ee) {

  ee.on('query', function(e, write) {
    // handle event request
    write([{ foo: 'bar' }]);      
  });

  ee.on('create', function(e, write) {
    // insert e.object into db
    write({
      id: 1,
      ok: true
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

