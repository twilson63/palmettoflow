# Global Application State

The concept of a global application state that is the `DNA` of an exact representation of your app in a give state in time.  By thinking in terms of global state and virtual transitions based on state change, you should be able to create snapshots of your application over time and re-play them on another device that has your application loaded.

The state is an observable structure that stores complex data and triggers notifications when changed or can be diffed in some loop to determine if changed and trigger a repaint of the application.  

## Examples

[TODO]