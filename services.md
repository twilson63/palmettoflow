<img src="palmetto.png" alt="palmetto" align="right" height="100px" width="100px" />

# Services

The service is responsible for business logic and data persistence, each service controls their own data store.  When registering a service it is important that the service can only listen to data events and submit/emit events from the write log.  This is how it communicates with the outside world.

``` js
module.exports = myservice;

function myservice() {
  
}