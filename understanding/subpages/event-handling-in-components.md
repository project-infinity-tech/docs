# Event Handling in Components

*This is “current” as at December 2024. The handling of how payloads work will probably be changed at some point, so these are the workarounds for now.*

In order to have “events” (such as a button being clicked) in a composite, we need to be able to use the “Emit Event” action along with the Composite Event definition.

Infinity already has built in events for things like Buttons, so you have “On Click” events that can be handled. However, these events are INSIDE the Composite Component and are not exposed when that Component is placed on a page. In the same way that not every property on every component is exposed when it is placed on a page (because you could have hundreds, and it would be overwhelming) not every event that happens in a component is exposed when placed on a page. 

When creating a Composite, you can define an “Event” in the Component Definition, which is the Logic Tab.

Here, we can add an Event that will be handled when the Component is placed on a Page by clicking the + next to Events.

![image.png](image%208.png)

So here we have two buttons in a “Button Group” Component. Each button has three events that we *could* handle (click, mouse enter, mouse leave), and the Container has the same three events. 

There would be a total of nine events that the component could potentially have, but to make things simpler and faster, we are only interested in someone clicking either of the two buttons.

*(note that if the user of the composite component wanted to handle something else, then they could clone the component and make changes).* 

We can therefore add a Composite Event 

So we can set up a Custom Event for the Primary Button being clicked….

![image.png](image%209.png)

And then we can set up the Cclick event on the Button to trigger the Custom Event.

![image.png](image%2010.png)

![image.png](image%2011.png)

![image.png](image%2012.png)

![image.png](image%2013.png)

![image.png](image%2014.png)