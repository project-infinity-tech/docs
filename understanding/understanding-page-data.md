# Understanding Page Data

Every Page in an Scram App can have some “Page Data” defined. You can find it at the bottom of the side menu.

Page Data is data that is loaded when the page is loaded. So it is there ready to be used on the page.

We define the data we want to use in our pages by setting up “Page Data Variables”. These variables can contain either a single data type, so something like a text, or a more complex type like a “Project” where a “Project” has multiple fields with your Project Data (name, start date, duration, who is managing). A “Project” can of course come from a database table but it could also come from an API that pulls in Project data. And you can even combine the two, so pull data from an external API and enrich with internal data. 

“Page Data Variables” can also be lists. So it could be a list of “Projects” that you are loading. 

Imagine you have a Project Management System that shows the User all the projects they have responsibility for. On the Dashboard you can load all their Projects, so that they are available to be displayed on the page. This would be a “Page Data Variable” with a Type of “List of Projects”.

Page data is loaded in a series of one or more “Steps” that combine into a “Workflow”. The simplest workflow is one Step that loads some data. But they can have multiple steps if needed. 

Each “step” in the page data workflow runs a particular “Action”

An Action can be -

- From a Data Source
    - An internal database query using Execute SQL
    - An API call that brings back data
    - The Scram Filestore
- Static data
    - You can, of course, load static as page data