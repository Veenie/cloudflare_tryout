# 👷 `worker-template` Hello World

A template for kick starting a Cloudflare worker project.

[`index.js`](https://github.com/cloudflare/worker-template/blob/master/index.js) is the content of the Workers script.

#### Wrangler

To generate using [wrangler](https://github.com/cloudflare/wrangler)

```
wrangler generate projectname https://github.com/cloudflare/worker-template
```

Further documentation for Wrangler can be found [here](https://developers.cloudflare.com/workers/tooling/wrangler).

Introduction
In this exercise, you'll learn to use Cloudflare Workers and Pages by creating your very own social media platform. The instructions below will guide you through the requirements.

Features
There are two parts to completing this project: a backend API, and a frontend web app.

Workers API
For the backend of this social media platform, you'll be using Cloudflare Workers to launch a serverless API which will allow the creation and storage of new posts, as well as distributing those posts to visitors of the site. To start, create a new Workers project with Wrangler. You'll need a free Cloudflare account for this.

Next, create a new Workers KV namespace (a simple key-value cloud storage environment), as this will be useful for the next step: storing a collection of posts.

API Endpoint 1: GET /posts
When the frontend queries /posts, it should receive a JSON response containing a list of post objects (obtained from your KV namespace) to be displayed on the platform.

Sample output (feel free to add more attributes to these objects):

[{"title":"My First Post", "username": "coolguy123", "content": "Hey Y'all!"}, {"title":"Story About my Dogs", "username": "kn0thing", "content": "So the other day I was in the yard, and..."}]

API Endpoint 2: POST /posts
This endpoint serves as the way to create a new post. It should take JSON input of the following form:

{"title": "foo", "username": "bar", "content": "blah" ... }

where any other required attributes are also found in the objects returned by endpoint 1. Hypothetically, one should be able to successfully submit a post object returned by endpoint 1.

A meaningful error message and status code should be returned if there are any problems posting, otherwise return 'success'.

Pages Frontend
Deploy a web app with Cloudflare Pages using a template such as Create-React-App.

Inside this web app, get the posts from your API and take the liberty to organize them in whichever way looks the best to you. It doesn't have to be perfect, but try to emulate the feel of a real social media platform.

Make some posts!
Test your application by creating a few posts with some information about yourself.

Extra Credit
If the previous steps were easy for you, we want you to showcase your talent to the fullest with these extra credit options!

User Posts
Add a series of inputs to your frontend which fill out the necessary information for a post and then submit that information to your POST endpoint to be added to the website.

Content Variety
A social media site is boring if the only available content is plain text -- photos, links, GIFs, and other forms of multimedia are all the rage these days. Add configuration options to each post allowing it to be presented differently depending on the type of content. Add some example posts of each type for us to see.

Interactivity
Just like allowing different types of content, a social media platform can gain a lot of value by allowing users to interact with the content they see. Here are some ideas:

Voting system which sorts the posts by their upvote/downvote scores
Emoji reactions
Comments section where users can give their opinions on posts by others
Move on to the Systems Assignment
The Systems Assignment, which uses the work that you've done here, is another great way to demonstrate your amazing developer skills to us. Show us what you've got!

Submitting Your Assignment
When you're done with your project, publish it on Workers and Pages!

After following the steps to get started, you should have received an email with submission instructions.

Clone the git repository generated for your general assignment
Copy the files from your Worker's project folder into "workers"
Copy the files from your Pages project's folder into "pages"
In the "info.txt" file, paste the URL to your published workers.dev project directly after the prompt (on the same line, leaving a space)
Repeat for your published pages.dev URL
Add everything, commit, and push!