
<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# Palmetto Flow

[![Join the chat at https://gitter.im/twilson63/palmettoflow](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/twilson63/palmettoflow?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## WIP - Work in progress, please star the project on github to keep informed.

[![ScreenShot](http://img.youtube.com/vi/INP1uuOYU3E/0.jpg)](http://youtu.be/INP1uuOYU3E)

Palmetto Flow is a concept for building applications.  

Palmetto Flow has a set of principals that enable you the developer to implement in technologies of your *choice*.

With Palmetto Flow developers can create applications made up of components and services that can be exchanged or modified overtime with different technology and approaches. 

The core concept is to separate your application using loosely coupled processes that all subscribe to a publish/subscribe system, then components can publish requests and services can subscribe to topics and process the requests.

* [Features](#features)
* [Benefits](#benefits)
* [Concepts](#concepts)
* [Discussion](#discussion)
* [Videos](#videos)
* [FAQ](faq.md)
* [Examples](examples.md)
* [Contribution](#contribution)
* [LICENSE](#license)

## Features

### Easy to understand

By structuring the application into components and services, it is easy for developers to understand and work together on features of the application.  Services live near and own the data, components live near and own the presentation.

### Re-Usability

By leveraging a publish/subscribe system services can serve many applications and components can be re-used in different applications.

### Developer Flexibility

Building Componenents or Services in any technology of choice create flexibility to empower developers to work in the best technology for the task and not worry about having to modify or infect other parts of the application.

## Benefits

### Scalability

Since publish/subscribe is one to many, you can have many subscribers for the same service over several different locations, or you can use a push/pull pattern to have several workers and balance the load of requests amongst all of the workers. You can implement all of the common messaging patterns on top of publish/subscribe

### Reliability

One of the key features of Palmetto Flow is the commit-log and the ability to replay the log to rebuild data sources from the beginning, creates a very reliable and stable data log, so if your service needs its data store rebuilt it is a very simple process.

### Feature Consistency

By separating the concerns of the application features Palmetto Flow can continue to keep timeline of adding a new feature consistent regardless of versions or iterations.  

## Concepts

* [Application State](state.md)
* [Write Stream](stream.md)
* [Components](components.md)
* [Services](services.md)
* [Adapters](adapters.md)

## Discussion

[https://gitter.im/twilson63/palmettoflow](https://gitter.im/twilson63/palmettoflow)

or submit an [Issue](https://github.com/twilson63/palmettoflow/issues)

## Videos

* [Intro Talk](http://youtu.be/INP1uuOYU3E)
* [Component Example](http://youtu.be/7TPC-tcIO4g)


## Contribution

see [contribution.md](contribution.md)

* [Contributors](https://github.com/twilson63/palmettoflow/graphs/contributors)

## License

see [LICENSE](LICENSE)
