# Understanding Page Data

Every Page in a Scram App can have some “Page Data” defined. You can find it at the bottom of the side menu.

Page Data is data loaded when the page loads. So it is there, ready to be used on the page.

We define the data we want to use in our pages by setting up “Page Data Variables”. These variables can contain either a single data type, such as a text, or a more complex type like a “Project” where a “Project” has multiple fields with your Project Data (name, start date, duration, who is managing). A “Project” can, of course, come from a database table, but it could also come from an API that pulls in Project data. And you can even combine the two by pulling data from an external API and enriching it with internal data.

“Page Data Variables” can also be lists. So it could be a list of “Projects” that you are loading.

Imagine you have a Project Management System that shows the User all the projects they have responsibility for. On the Dashboard, you can load all their Projects so they are available to display on the page. This would be a “Page Data Variable” with a Type of “List of Projects”.

Page data is loaded in a series of one or more “Steps” that combine into a “Workflow”. The simplest workflow is one Step that loads some data. But they can have multiple steps if needed.

Each “step” in the page data workflow runs a particular “Action”

An Action can be -

- From a Data Source
  - An internal database query using Execute SQL
  - An API call that brings back data
  - The Scram Filestore
- Static data
  - You can, of course, load static data as page data

Outputs

There are two ways to expose the result of 

- "Inherit" 
  - In this case the output 
- "Success" 