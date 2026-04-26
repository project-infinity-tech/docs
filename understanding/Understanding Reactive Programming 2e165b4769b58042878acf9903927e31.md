# Understanding Reactive Programming

### Or at least how Scram implements Reactive programming !

Scram's front end builds React Apps. If you already know about React then you will be familiar with Reactive Programming.

If not then buckle in for a quick tour.

Let's start with a very simple example. Let's say you have a component on your page that is displaying the First Name of your User and some data about the user.

Your component has a "Prop" which passes in the First Name (you could of course reference the first name directly by reading the database or user table but to make your components flexible in case your database changes, let's pass it in).

So you create a variable on your page to hold the first name, you pass this into the prop and it displays on the page.

Now, if you update that variable the Component "reacts" to the change in the prop, and displays the new name. And also any expressions that might be linked to that prop also recalulate. So maybe if there is no firstname you change the greeting.

So, instead of having to think "oh, my first name has changed, I better update the page" it all happens reactively for you.

Now imagine we have several components, that we are passing the first name to (we are very friendly and like to greet our users a lot) then we can point the props of all those components to the same variable. When that changes they all automatically recalculate.

OK, so that is a very simple example, but we could have a list of outstanding invoices and we are holding the "current" invoice we are working on in a variable and we pass this to the components. The main component updates to show the current invoice, and another shows the list you are working on and highlights the current one.

Reactive programming means that you don't need to worry about your components updating when data changes. Scram components are reactive. They change when their data changes.