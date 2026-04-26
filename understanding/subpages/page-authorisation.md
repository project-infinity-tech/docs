# Page Authorisation

Every page in your app has the ability to be "protected" so that only some users can view or interact with that page. This is linked to a User being signed in and having a role that you control.

You do that in the page settings by switching on **"Requires Authentication"**. Once you turn that on, you then get a selector where you can choose which User roles can view that page.

**NOTE:** If you turn on "Requires Authentication" but don't assign any roles to a page, then NOBODY can see that page - not even logged-in users. So make sure you select at least one role, or turn off authentication entirely if you want the page to be public.

In order to let different types of User access different pages, you can have different roles assigned. In Scram, Users can have multiple roles, and Pages can have multiple roles allowed, so you have a lot of flexibility in how you set up your page authorizations. A User only needs ONE of the allowed roles to access a page.

If a User tries to access a page for which they don't have the required role, then by default they will be taken to your home page (your root page with path `/`). You can change this behavior in the App Settings where you can specify which page the user should be redirected to. So you can create a "Whoops, you don't have authority to access that - contact your administrator" page and redirect them to that. Or just use the home page by default, your choice.

Note that the same Authorisation Roles described here[Understanding User Management](Understanding%20User%20Management%202e165b4769b580139e47de2d32b229bc.md) are also used in [Workflow Auth](Workflow%20Auth%202ee65b4769b580149556f93b124fc4b7.md) 

## Example

You might have a 'Dashboard' page that requires authentication with 'User' role, and an 'Admin Panel' that requires the 'Admin' role."

*TIP: Want a public landing page? Just leave 'Requires Authentication' turned OFF, and anyone can visit it."*