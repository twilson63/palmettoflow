# Palmetto Flow

## WIP - Work in progress, please star the project on github to keep informed.

Palmetto Flow is a concept about building applications.  Palmetto is a set of principals that enable you to implement in technologies of your choice.  The goal is to create applications, components and services that act like stereos, it is very easy to replace pieces of the application without having to replace/re-write the entire application.  There are a few concepts to understand and they should be straight forward and simple to follow:

## [FAQ](faq.md)

* [Application State](state.md)
* [Write Stream](stream.md)
* [Events](events.md)
* [Components](components.md)
* [Services](services.md)

## Features

### Easy to understand

By structuring the application into components and services, it should be easy for developers to understand and work together on features of the application.  It should be straight forward where code should live on a component or service.

### Re-Usability

Componenents can be built into component trees and be reused in several different applications, especially if you follow a pattern of seperating your pure components from your state components, this will increase the re-usability of your components.

### Developer Flexibility

Building Componenents or Services in any technology of choice create a lot of flexibility to enable several developers to work on the same and similiar applications without having to learn complex methodologies.

## Benefits

### Scalability

The ability to cluster, shard or distribute can be placed on your stream system and your services can run as many instances.

### Reliability

The ability to bring up a service by replaying the log is a very powerful concept which gives you a strong recovery plan as well as migration plan.

### Feature Consistency

By separating the concerns of the application features it should continue to keep timeline of adding a new feature consistent regardless if this is feature 3 or feature 303.  The amount of time to add/modify/remove features should not slow down exponentially over time.  Also, it should make it easy to remove features that do not work and are not being used just as easy as adding new features.