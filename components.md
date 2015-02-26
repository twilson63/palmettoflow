<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Components

A `Component` in palmetto flow is responsible for the rendering the state of a section of your application as some sort of presentation view.  In most applicaitons this would be html.  The component is also responsible for listening to events that may effect the change in state for your component.  The component is also capable of posting events into a write log/stream to either add data to a service or query data from services.

## Features

### Event Emitter (pub/sub)

So the component should handle all of it communications with others via the `EventEmitter` or pub/sub.  When new route request comes in, it will recieve the request adjust the state and set the 'ref' node for the state to the component to create a change event and notify the system that the page needs to be rendered.

``` js

function(state,ee) {
  ee.on('/home', function() {
    state.set('ref', '/home');
  });
}
```


### Pure Render

``` js
function (state) {
  return h('h1', 'Hello World')
}
```
