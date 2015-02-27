<img src="palmetto2.png" alt="palmetto" align="right" height="100px" width="100px" />

# State

State is the data that is being used to drive the presentation at this current instant.  I think of it as the DNA to the application for a give situation.  The ideal implementation of palmettoflow, is on that you can extract the current state at a given point.  Take that data and insert it into another browser of the same application and see the exact same result.

A good example of this is this video from circle ci: https://www.youtube.com/watch?v=5yHFTN-_mOo 

Now they are using clojurescript and om, but this concept of immutable state is borrowed from clojure.

Mercury and the Virtual-DOM share this concept of a global state tree, and when something changes on that tree, a render is triggered.  The render code is a tree full of pure functions and it generates the full html view in a json vtree format.  This is passed to the virtual-dom engine which performs a diff between the current view of the dom and calculates the differences.  Then it just asks the browser to modify the differences.  This enables the developer to reason about the presentation of their application in a scene by scene basis and it is much easier to debug and test.

I think you can do a very similar thing with two-way databinding frameworks like angularjs and vue, but I have yet to experiement, I think some others are experiementing with this concept.


