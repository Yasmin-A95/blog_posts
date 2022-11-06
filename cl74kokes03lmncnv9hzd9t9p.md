# Express Quickie

#### Express, What?

Express is a [self-identified](https://expressjs.com/) minimalist web framework for Node.js. Cool. In my own words as an uncool baby software dev who doesn't mess with all that jargon just yet, it's a server. Proper devs feel free to bully me in the comments. 

#### Express, How?

Run the `npm init -y` command in the terminal if you're starting from scratch to get your package JSON without answering a bunch of annoying questions. If you don't know what I'm talking about, try dropping the -y and running that same command. Make your files and then `npm install express`. 


Throw this at the top of your scripts file to import express. 
```
const express = require('express');
const server = express();
```
Then sort out your routes. They can go on and on like the example below for as many pages as you'd like, but if you find you're making a lot of them, express might not have been the best option. 
```
server.get('/', (req, res) => {
          res.send("Wow what a great website)
});
```

At the end of your scripts file, throw on this with a console.log for comfort's sake. 
```
server.listen(PORT, () => {
           console.log(`Now serving on http://localhost:${ PORT }`)
});
```
If you use to express a couple of times, you will one day forget to add this and be staring into your terminal wondering what's wrong when everything's a-ok. You won't remember this blog post, and you may even break something trying to 'fix' the problem. Good luck with that, and goodbye. 
