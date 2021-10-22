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

Cloudflare Systems Assignment: JWT Jam!
Introduction
So you've just completed your awesome general assignment and now you've come here to go the extra mile and show off some skills. This assignment is more low-level, a little more involved, and in our opinion, makes you feel a lot cooler when it works.

We expect this assignment to take around 2-3 hours, but we totally understand how busy this season is for all of you. So please feel free to submit a partial solution if you're pressed for time, we'll still look at it! On the other hand, if you can knock out the main part of the assignment in just an hour or two, we encourage you to try some extra credit options to go above and beyond.

Backstory
We really believe in your new social media platform, but right now, you can't tell who is posting what. What you need is some way to authenticate users' identities with a token, so that one user can't pose as another by spoofing their username.

We're going to skip the process of checking usernames and passwords and go straight to the token step: once a user's identity has hypothetically been confirmed, you are responsible for creating, distributing, and validating tokens for the users of your platform.

Technology Involved
JWT (pronounced "jot")
JWTs are tokens which contain cryptographically signed information -- but not encrypted -- about a user's identity, effectively authenticating them. This is the alternative to sending a user's password around with every request to every microservice in your application.

You will be using the RS256 algorithm for signing and decoding your JWTs -- so that every microservice can perform validation with a public key without needing access to the super-secret private key. For this you'll need an RSA key pair, so generate one before you start.

One of these low-level languages
Don't worry if you aren't yet familiar with these languages! Many engineers join Cloudflare without specific language experience. We've provided links to helpful guides for each language. If you're just learning a language for the first time, that won't hurt your score at all.

Rust
Learn Rust by reading the book, or by example.

We recommend using warp or actix-web to serve the HTTP requests, and jsonwebtoken for processing the JWT

Go
A Tour of Go and Go by Example are great resources.

Go's own net/http is a good HTTP library, or use chi for some added flexiblility. jwt-go provides JWT tools

C/C++
Learn C, or perhaps learn C++ by example.

cpp-httplib can be used to route and handle requests, while jwt-cpp provides helper functions for JWTs

Tasks
HTTP server
Your HTTP API will have a few endpoints, which are detailed below. Requests to paths other than these should receive a 404.

Endpoint 1: GET /auth/<username>
This endpoint creates a JWT and sends it back to the user as a cookie. The body of the response should simply be your RSA public key in plain text.

JWTs should have the claim sub=<username> and should expire exactly 24 hours after being issued. The JWT cookie should be named "token", should NOT be accessible by client-side JavaScript, and should be visible to all paths on the server.

Endpoint 2: GET /verify
This endpoint receives a cookie from the user and verifies that it is signed and unexpired. If the token provided was legitimate, return their username as plain text. If the token could not be verified for any reason, return a meaningful error message as plaintext and a corresponding meaningful HTTP status code.

Bonus - Endpoint 3: GET /README.txt
This endpoint simply loads your short write-up from a file and serves it to the user as text, so they can read about your project. Instructions for the README are below.

Bonus - Endpoint 4: GET /stats
Record each time a user visits /auth and /verify and display this information. Time each JWT encoding and decoding operation and average them. Present this however you want, but keep it simple.

Extra Credit: Integration with General Assignment
You've made this cool JWT authentication service, so now it's time to tie it into your general assignment. We will create a system which ensures that two posts with the same username were created by the same person.

Follow the setup for "Grading your Project" below
You'll want to create a Cloudflare tunnel for your API so that your frontend assignment can easily access it from the internet. Just make sure not to accidentally close this tunnel, or the name will change.

Identify your users
First, you will need the ability store a collection of usernames in your Workers KV namespace from earlier, and prevent users from posting with a username which has already been taken.

Handle new usernames
If a user creates a post with a new username, send a request from your worker to https://<tunnel>.trycloudflare.com/auth/<username> and forward the resulting Set-Cookie header into your worker's response. This cookie duplication could be avoided by hosting the frontend and backend on the same domain name, but for this simple application we won't worry about it.

Handle existing usernames
If a user tries to post under a username which already exists, but the poster owns a JWT with that username, then that user should be allowed to post under their own name. Check this by forwarding the Cookie header from the request to https://<tunnel>.trycloudflare.com/verify and checking that it returns successfully with the right username. If not, don't make the post.

With this, users will effectively get 'locked out' from their username once their JWT expires: after one day. Don't worry about whether this makes sense -- it's a feature. Let's call it "flash accounts" or something.

Write a README.txt
Create a short write-up to tell us about your work.

What new knowledge or skills did you take away from this project? If you learned a new language for this assignment, make sure to tell us.
What was the most difficult part of this assignment?
Did you attempt any extra credit? Tell us what you chose
Grading your Project
To give us the best way to evaluate your submission, visit our Systems Assignment Autograder and follow the instructions to automatically score your assignment and even get instant feedback if anything didn't work correctly.

Submitting your Assignment
After following the steps to get started, you should have received an email with submission instructions.

Clone the git repository generated for your systems assignment
Copy the files from your project folder into the git repository
Make sure that your README.txt file is in there
Add everything, commit, and push!
Pat yourself on the back
We're very proud of you for getting this far, and thank you so much for applying to Cloudflare!